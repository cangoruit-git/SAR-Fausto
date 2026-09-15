# ADR-0003 — Cifrado en tránsito y reposo, sin custodia de claves por cuenta

**Estado:** ACEPTADA
**Fecha:** 2026-09-15
**Decide:** `QD-004`
**Depende de:** ADR-0001, ADR-0002
**Resuelve:** `OQ-003`
**Enmienda:** ADR-0001, mitigación #3

---

## Contexto

`ADR-0001` estableció dos cuentas independientes y `ADR-0002` estableció despliegue en nube. Esa combinación produce un hecho incómodo: **los datos privados de A y de B conviven en la misma base de datos**, y la frontera entre ambos ya no la garantiza el dispositivo sino el código.

`QD-004` preguntaba si además existe una **barrera criptográfica independiente del código**. Es decir: quién puede convertir el cifrado en texto claro.

## Decisión

Se adopta la opción **(d): cifrado estándar en tránsito (TLS) y en reposo, sin custodia de claves por cuenta.**

1. Las claves las administra la infraestructura. No hay claves derivadas de la cuenta ni claves del usuario.
2. **El operador puede leer el contenido.** No es un efecto secundario: es la consecuencia directa y reconocida de esta decisión.
3. Se utiliza un proveedor externo de modelo de lenguaje, bajo contrato de **retención cero y sin entrenamiento sobre los datos**.
4. El análisis (patrones, memoria temporal, generación de hipótesis) corre en servidor.

## Consecuencias

### Positivas

- **El costo y la latencia más bajos** de las cuatro opciones evaluadas.
- Habilita el análisis en servidor sin fricción: los patrones a lo largo del tiempo, la memoria temporal y la búsqueda funcionan sin depender del hardware de la persona.
- **No hay gestión de claves**, y por lo tanto no existe el problema de la clave perdida que deja a alguien sin acceso a su propia historia.
- Es la opción más rápida de construir, lo que permite llegar antes a la validación del producto.

### Negativas — costos asumidos explícitamente

1. **Cero barrera criptográfica.** `INV-PRIV-001` ("ningún dato de A es legible por B") pasa a depender **exclusivamente** de código de aplicación y de políticas de base de datos. Una sola capa, sin respaldo independiente.
2. **Se elimina la mitigación #3 de ADR-0001.** Ese ADR listaba "claves de cifrado por cuenta como segunda barrera independiente del código de aplicación". Con esta decisión **esa barrera no existe**. Quedan: aislamiento a nivel de fila, tests por frontera, y disciplina de código. Ver la enmienda más abajo.
3. **`THR-OPERATOR` deja de ser mitigable por criptografía.** El personal de soporte, operaciones o cualquiera con acceso a la base puede leer contenido íntimo. Solo se mitiga por diseño de herramientas, auditoría y minimización — nunca por matemática.
4. **`THR-LEGAL` se materializa.** Si un juez lo requiere, el operador **debe** entregar el contenido. `G-SAFE-5` deja de ser un aviso general y pasa a ser una obligación de transparencia destacada.
5. **Los respaldos contienen texto claro.** Toda copia —respaldo, réplica, entorno de staging, volcado de base para depuración— es una copia legible de datos íntimos.
6. **Un incidente de seguridad es una brecha de datos de categoría especial** (salud y vida sexual), con las obligaciones de notificación que eso implica.
7. **La retención pasa a ser la palanca principal de protección.** Si el operador puede leer todo, lo que más protege es que **exista la menor cantidad posible de contenido, durante el menor tiempo posible**.

### Enmienda a ADR-0001

ADR-0001, sección "Advertencia de arquitectura", mitigación #3 queda **sin efecto**. Las mitigaciones vigentes pasan a ser:

1. `INV-PRIV-001..010` implementados y testeados por frontera **antes** de que entre cualquier dato real.
2. Aislamiento a nivel de fila en la base de datos, no solo en la capa de aplicación.
3. ~~Claves de cifrado por cuenta~~ → **reemplazada por**: costura de cifrado única (ver más abajo), soporte sin acceso a contenido, y auditoría de acceso interno.
4. La suite `tests/privacy/` como requisito de merge, no como backlog.

## Controles compensatorios — obligatorios

Con esta decisión, lo único que separa el sistema de "el operador lee la intimidad de las parejas" es el siguiente conjunto. **No son recomendaciones: son requisitos de G4.** Si alguno no se implementa, esta decisión debe revisarse.

| Control | Descripción |
| --- | --- |
| `RET-###` — retención máxima | Ventana de retención declarada por tipo de dato, con **borrado automático y verificable**. Sin retención indefinida. Default corto, no largo |
| Aislamiento a nivel de fila | En la base de datos, testeado, no solo en la capa de aplicación |
| Soporte sin contenido | Las herramientas internas devuelven IDs y metadatos operativos, **nunca texto**. Prohibido el acceso humano a contenido en claro salvo excepción declarada y auditada |
| Auditoría de acceso interno | Todo acceso privilegiado se registra: quién, cuándo, qué registro. Sin volcar contenido al log |
| Prohibición de datos reales fuera de producción | Desarrollo, staging, pruebas y demos usan datos sintéticos. Sin excepciones |
| Sin terceros con contenido | Nada de analítica, crash reporting ni servicios externos con contenido o identificadores estables |
| Transparencia explícita | Antes de la primera captura se declara que el operador puede leer el contenido y que puede ser compelido a entregarlo |
| DPIA bloqueante | Con esta postura declarada, la DPIA es condición de entrada a cualquier dato real |
| `tests/privacy/` | Requisito de merge desde el primer commit con datos |

## Requisito de reversibilidad — costura de cifrado

Esta decisión es barata ahora y **cara después solo si se construye mal**. Por eso se establece un requisito de arquitectura para G5:

1. **Todo acceso a contenido pasa por un único módulo** ("costura de cifrado") que recibe cuenta + dato y decide cómo leerlo y escribirlo. Hoy ese módulo usa la clave de infraestructura.
2. Si más adelante se decide pasar a `(a)`, `(b)` o `(c)`, se cambia **ese módulo** y se ejecuta una migración de datos. El resto del sistema no se toca.
3. **Prohibido:** que el acceso a contenido esté disperso por el código, o que el modelo de datos asuma que el contenido es legible globalmente.
4. **Consecuencia para `DATA_MODEL_V1.md` (G5):** cada campo debe declararse como `CONTENT` (pasa por la costura) o `METADATA_OPERATIVO`. El análisis de patrones debe declarar si necesita texto claro o si puede operar sobre derivados.

Esta costura es lo que mantiene la decisión **reversible** en lugar de estructural.

## Riesgo residual aceptado

**`RISK-001` — El operador, su personal y quien lo obligue legalmente pueden leer contenido íntimo de personas reales.**

Se acepta conscientemente a cambio de menor costo, menor latencia y mayor velocidad de construcción. El riesgo se **reduce** —no se elimina— mediante retención corta, minimización, ausencia de acceso humano a contenido, auditoría de acceso y transparencia.

Condiciones de revisión obligatoria:

- antes de `QD-007` (piloto con personas reales);
- si aparece un requisito de cumplimiento normativo en la jurisdicción elegida;
- si cambia el alcance del producto (`QD-005`);
- si el sistema llega a menores de edad: se detiene, no se mitiga.

## Lo que esta decisión NO decide

- Las ventanas concretas de retención: G4 (`RET-###`).
- El proveedor de modelo y la región: G5.
- Si el MVP usa modelo de lenguaje externo o solo análisis determinista: sigue abierto dentro de esta opción.
- El alcance del producto: `QD-005`.
