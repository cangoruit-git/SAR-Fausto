# ADR-0001 — Dos cuentas independientes, una por persona

**Estado:** ACEPTADA
**Fecha:** 2026-09-15
**Decide:** `QD-002`
**Depende de:** —
**Relacionada con:** ADR-0002

---

## Contexto

El sistema relaciona a **dos personas autónomas** y una relación que emerge entre ellas. La decisión `QD-002` preguntaba cómo se materializa esa separación en cuentas y dispositivos:

- (a) una cuenta compartida en un dispositivo compartido;
- (b) dos cuentas independientes, cada persona en su dispositivo;
- (c) híbrido.

Esta decisión **define todo el modelo de privacidad y de amenazas**, porque determina dónde está la frontera entre lo privado de A y lo privado de B: en la física de los dispositivos, o en el código.

## Decisión

Se adopta **(b): dos cuentas independientes**, una por persona, cada una operable desde su propio dispositivo.

1. Cada persona tiene su propia identidad, sus propias credenciales y su propio espacio de datos.
2. **Lo privado es el estado por defecto de todo dato.** Nada es visible para la otra persona por el hecho de existir.
3. No existe una "cuenta de pareja". La relación es un vínculo entre dos cuentas, no una tercera cuenta.
4. La relación solo puede contener elementos que **ambas partes publicaron explícitamente** o que ambas aceptaron explícitamente.

## Consecuencias

### Positivas

- **Nadie puede ser vigilado por el otro desde el sistema**: no hay una superficie donde B pueda observar qué hace A. Esto elimina de raíz una clase entera de uso abusivo y es coherente con `PRIN` de autonomía y con `G-SAFE-1`.
- El consentimiento se vuelve un **acto explícito entre dos cuentas**, no un estado implícito de "estar casados en la app".
- La asimetría de información que suele aparecer en productos de pareja no se puede construir por accidente.

### Negativas y costos asumidos

- **Se pierde la comodidad del espacio compartido "gratis".** Todo lo compartido debe construirse por acto explícito. Eso es más trabajo de diseño, no menos: hay que definir un protocolo de publicación, aceptación y revocación.
- La vinculación entre cuentas es, en sí misma, **información revelada**. Ver "Lo que esta decisión obliga", punto 3.

## Lo que esta decisión obliga

1. **`G-SAFE-3` (modo dispositivo compartido) NO se elimina.** Dos cuentas no significan dos dispositivos siempre: las parejas comparten teléfonos y tablets, y un tercero puede tener la contraseña. El modo compartido deja de ser la arquitectura por defecto y pasa a ser un **modo explícito** con sus propios defaults. Sigue siendo obligatorio.

2. **El espacio compartido es construido, nunca inferido.** Con dos cuentas aisladas, nada "pertenece a la relación" salvo que ambas partes lo hayan publicado o aceptado. Consecuencia directa: **ningún artefacto derivado de datos privados puede entrar al espacio compartido** — ni siquiera "porque es solo una inferencia". Esto convierte `INV-PRIV-002` (la visibilidad de un derivado es la intersección de la visibilidad de sus insumos) en una **propiedad estructural** en lugar de una política que hay que recordar aplicar.

3. **La vinculación es una revelación y debe modelarse como tal.** Invitar a la otra persona revela que uno usa el sistema. Aceptar revela lo mismo en el otro sentido. Ambas son irreversibles. El sistema debe:
   - no revelar nada antes del acto explícito de invitar (usar el sistema solo no filtra nada hacia el otro);
   - registrar la vinculación como un evento de consentimiento bilateral;
   - decidir explícitamente qué ocurre al **desvincularse** (ver `OQ-002`).

4. **Los indicadores de actividad entre cuentas deben ser imposibles, no solo ocultos.** "B no registró nada en 6 días" es fuga de metadatos (`INV-PRIV-003`) **y** presión relacional. Regla de diseño: **no existe ningún contador, indicador ni estado de participación cross-account.** Se implementa por ausencia de la superficie, no por una verificación que pueda fallar.

5. **La eliminación de una cuenta es bilateral y hay que decidirla.** Si A elimina su cuenta, ¿qué pasa con un acuerdo que ambos aceptaron, o con el resultado de un experimento conjunto? Ver `OQ-001`.

6. **El uso asimétrico es esperable y no debe castigarse.** Dos cuentas hacen más probable que una persona use el sistema mucho y la otra poco. El sistema no debe señalizarlo, ni sugerirlo, ni usar la participación como medida de compromiso con la relación.

## Lo que esta decisión NO decide

- No decide dónde viven los datos: eso es **ADR-0002** (nube).
- No decide dónde se procesa el contenido: eso es `QD-004`.
- No decide qué categorías de dato son compartibles: eso se define en `docs/privacy/PRIVACY_MODEL.md` (G1).
- No decide el alcance del producto: `QD-005` sigue abierta.

## Advertencia de arquitectura

**Con dos cuentas y datos en un mismo servidor, la separación entre A y B deja de estar garantizada por la física y pasa a depender del código.** Esa es la consecuencia más importante de esta decisión combinada con ADR-0002: el eslabón más débil deja de ser el dispositivo y pasa a ser un control de acceso mal escrito.

Mitigaciones obligatorias, en orden de implementación:

1. `INV-PRIV-001..010` implementados y **testeados por frontera** antes de que entre cualquier dato real.
2. Aislamiento a nivel de fila en la base de datos, no solo en la capa de aplicación.
3. Claves de cifrado por cuenta (ver `QD-004`) como segunda barrera independiente del código de aplicación.
4. La suite `tests/privacy/` como **requisito de merge**, no como backlog.

## Preguntas abiertas derivadas

- `OQ-001` — ¿Qué ocurre con los artefactos compartidos cuando una cuenta se elimina?
- `OQ-002` — ¿La desvinculación se comunica de inmediato o se difiere?
