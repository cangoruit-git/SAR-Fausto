# ADR-0004 — Distribución: código abierto autohospedado como vía primaria

**Estado:** ACEPTADA
**Fecha:** 2026-09-15
**Decide:** modelo de distribución; y `QD-001` en lo relativo a licencia y visibilidad
**Depende de:** ADR-0001, ADR-0002, ADR-0003

---

## Contexto

Tres decisiones previas produjeron una situación con una tensión sin resolver:

- `ADR-0001` — dos cuentas independientes: la separación entre A y B depende del código.
- `ADR-0003` — sin custodia de claves por cuenta: **el operador puede leer** (`RISK-001` aceptado).
- El objetivo declarado del proyecto incluye que el sistema pueda ser útil a **muchas parejas**, no a una.

Un servicio gestionado por el proyecto, con la postura de `ADR-0003`, significa que quien opera el sistema puede leer la intimidad de personas que no conoce, con obligación legal de entregarla si un juez lo requiere. Y al mismo tiempo, la única forma de alcanzar a muchas parejas sin recolectar su intimidad es que **cada pareja opere su propia instancia**.

## Decisión

1. **El repositorio es público** y el sistema es software libre bajo **AGPL-3.0**.
2. La vía de distribución **primaria** es el **autohospedaje**: cada pareja corre su propia instancia, en su propio equipo o servidor.
3. **Un servicio gestionado no es la vía primaria.** Puede existir más adelante —operado por el proyecto o por terceros— y si alguien lo ofrece como servicio en red, AGPL le obliga a publicar su código completo.
4. El proyecto **no recolecta datos** de las personas que autohospedan.

## Consecuencias

### Positivas

- **`RISK-001` deja de aplicar a la vía primaria.** El operador es la pareja. No hay un tercero que pueda leer.
- **El proyecto deja de ser custodio de datos íntimos ajenos.** En la vía primaria, cada pareja es responsable de su propia instancia y de sus propios datos. Esto reduce de forma sustancial la exposición legal y la obligación de DPIA *por parte del proyecto*.
- **Auditabilidad real.** Con `ADR-0003`, la garantía de privacidad depende únicamente de código. Publicar el código es lo que permite que un tercero verifique esa afirmación. **El repositorio público es el control compensatorio que faltaba para `RISK-001`.**
- **AGPL es lo que vuelve segura la estrategia de alcance.** Quien quiera llegar a muchas parejas con un servicio puede hacerlo — pero con el código publicado. Nadie puede quedarse con la intimidad de las parejas dentro de una caja negra.

### Negativas y costos asumidos

1. **El alcance queda limitado por la fricción del autohospedaje.** "Muchas parejas" no ocurre por sí solo: hoy el sistema solo llegaría a parejas con comodidad técnica. Resolverlo es un **problema de producto** —empaquetado, instalación en un comando, distribución simple— y no se resuelve con intención. **Este es el costo principal de esta decisión y debe nombrarse cada vez que se hable de alcance.**
2. **Sin soporte.** No hay garantía ni atención. Los problemas se reportan en el repositorio.
3. **Sin telemetría**, porque `INV-PRIV-005` la prohíbe y `ADR-0003` la haría peligrosa. El proyecto **no sabrá** cómo se usa el sistema ni cuándo falla. El aprendizaje sobre el producto depende del reporte voluntario. Esto limita la capacidad de validar la hipótesis central del proyecto (`Spec` §69).
4. **AGPL reduce la adopción** por parte de terceros que quisieran cerrar el código.
5. **La documentación pasa a ser artefacto de producto de primera clase**: guía de instalación, de respaldo, de actualización y de verificación de privacidad. En un producto de privacidad autohospedado, la documentación **es** el producto.

## Riesgo nuevo — `RISK-002`: asimetría de administración

**En autohospedaje, quien instala la instancia tiene acceso a todo.** Si una sola persona de la pareja la instala y la administra, obtiene exactamente el poder que tenía el operador en `ADR-0003` — y la otra persona no necesariamente lo sabe.

Dato duro: **el autohospedaje no es simétrico por defecto.** Resuelve el problema frente a terceros y no lo resuelve frente a la pareja.

| Mitigación | Tipo |
| --- | --- |
| Advertencia explícita en la guía de instalación: "quien administra esta instancia puede leer todos los datos" | Documental — obligatoria |
| Instalación hecha por ambas personas, o con la otra presente | Proceso |
| **Claves por cuenta** (opciones (a)/(b) de `QD-004`) | Técnica — la única configuración en la que **tampoco el administrador puede leer** |

**Consecuencia para `QD-004`:** la postura elegida en `ADR-0003` rige para el despliegue operado por el proyecto. Para el perfil autohospedado, **la única configuración verdaderamente simétrica es el cifrado con claves por cuenta**. Se registra como `OQ-004` para revisar en G5, sin modificar `ADR-0003`.

**Consecuencia para la costura de cifrado:** sigue siendo obligatoria y ahora es *más* importante, porque es lo que mantiene alcanzable el único despliegue donde nadie —ni el operador, ni el administrador de la instancia— puede leer.

## Requisitos no funcionales que esta decisión impone (G4)

| Requisito | Umbral |
| --- | --- |
| Instalación | Un comando |
| Capacidad de equipo | Funciona en un equipo de capacidad modesta (Raspberry Pi, VPS de gama baja) |
| Respaldo y restauración | Realizable por una persona no experta |
| Actualización | Sin pérdida de datos |
| Modelo de lenguaje | `BYO` API key o modelo local; sin dependencia de un servicio del proyecto |
| Telemetría saliente | Ninguna |
| Verificación de privacidad | El operador de la instancia debe poder comprobar que nada sale |

## Lo que esta decisión NO decide

- Si existirá un servicio gestionado. Si existe, `RISK-001` vuelve con fuerza y exige `RET-###`, aislamiento por fila, auditoría y DPIA antes del primer dato.
- Si el MVP usa modelo de lenguaje externo o análisis determinista.
- La región de despliegue (relevante solo si existe servicio gestionado).
- El significado literal de la sigla "SAR": ver `OQ-005`.
