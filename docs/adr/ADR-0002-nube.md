# ADR-0002 — Despliegue en nube

**Estado:** ACEPTADA
**Fecha:** 2026-09-15
**Decide:** `QD-003`
**Depende de:** ADR-0001
**Relacionada con:** ADR-0001

---

## Contexto

`QD-003` preguntaba dónde viven los datos:

- (a) local-first, sin nube;
- (b) nube con cifrado;
- (c) híbrido.

Esta decisión determina quién es el custodio del dato más sensible del sistema: contenido íntimo de una relación, que en varias jurisdicciones cae en **categoría especial** (salud y vida sexual). No es una decisión de hosting: es una posición regulatoria y ética.

## Decisión

Se adopta **(b): despliegue en nube.**

Los datos de las cuentas viven en infraestructura operada por el proyecto. La persona usuaria no custodia el único ejemplar de su información.

## Consecuencias

### Positivas

- Sincronización, respaldo y acceso desde cualquier dispositivo sin que la persona administre nada.
- Es la única forma de que el análisis agregado a lo largo del tiempo (memoria temporal, patrones) sea consistente entre sesiones y dispositivos.
- Habilita el procesamiento en servidor, que es más barato que el cómputo en el dispositivo para la mayoría de las personas.

### Negativas y costos asumidos

1. **El operador pasa a ser custodio de datos de categoría especial.** Esto no es opcional: implica base legal, registro de tratamiento, política de retención, procedimiento de brecha, y **DPIA obligatoria antes de cualquier dato real** (ya exigida en el Plan v2 §9.4, ahora con carácter bloqueante).
2. **La confianza se traslada del dispositivo al código, a los operadores y a la infraestructura.** Ver ADR-0001, "Advertencia de arquitectura". Con nube no hay segregación física que respalde la separación entre A y B: **`INV-PRIV-001..010` son el único muro.** Dejan de ser criterios de calidad y pasan a ser la estructura portante del sistema.
3. **Aparece el adversario interno.** El personal de soporte, operaciones o cualquier persona con acceso a la base puede leer contenido íntimo. Esto **amplía el modelo de amenazas** con un adversario que no estaba contemplado:
   - `THR-OPERATOR` — acceso interno a la base de datos o a los respaldos.
   Control exigido: aislamiento a nivel de fila, claves por cuenta, acceso interno auditado y minimizado, y **prohibición de acceso a contenido en claro para soporte** (el soporte opera sobre IDs, nunca sobre texto).
4. **Exposición legal.** Los datos pueden ser alcanzados por un requerimiento judicial. `G-SAFE-5` deja de ser un aviso abstracto y se convierte en una obligación concreta de transparencia: hay que decir explícitamente a las personas que el operador puede ser compelido a entregar su información. La única mitigación real es la postura de cifrado de `QD-004`.
5. **Los respaldos son una superficie de riesgo nueva.** Un respaldo contiene exactamente los mismos datos íntimos, con la misma obligación de separación. Los procedimientos de restauración deben verificar los invariantes de privacidad, no solo la integridad de los datos.
6. **La observabilidad pasa a ser peligrosa por defecto.** En nube, logs, trazas y métricas existen y por defecto contienen contenido. `INV-PRIV-005` debe aplicarse **en la capa de logging desde el primer commit** y verificarse con el test `tests/no_content_logs`, no agregarse después.
7. **Aparecen obligaciones no funcionales**: disponibilidad, latencia, costo por cuenta, residencia de datos y procedimiento de brecha.
8. **Se pierde el funcionamiento sin conexión** salvo que se diseñe explícitamente. Ver `NFR-###` en G4.

## Lo que esta decisión obliga

1. **Orden de implementación invertido respecto de un producto normal.** Primero la columna vertebral de privacidad (aislamiento, cifrado, logging sin contenido, tests por frontera); después las funcionalidades. Ninguna funcionalidad entra en nube antes de que `tests/privacy/` pase.
2. **`THR-OPERATOR` se incorpora al modelo de amenazas** de G1 (`docs/security/THREAT_MODEL.md`), junto a `THR-CLOUD` y `THR-LEGAL`.
3. **Ampliar `INV-PRIV-005`** para cubrir explícitamente los respaldos y el acceso interno de soporte, no solo logs y telemetría.
4. **Residencia y jurisdicción** deben decidirse y declararse antes de que entre el primer dato real.
5. **DPIA bloqueante**: sin `DPIA-lite.md` aprobada no se habilita un entorno con datos de personas reales.

## Lo que esta decisión NO decide

- **No decide dónde se procesa el contenido.** Almacenar en nube y procesar en nube son decisiones distintas. Esa es `QD-004`, y ahora es la pregunta que **determina si el operador puede leer el contenido o no**.
- No decide el proveedor, la región ni la tecnología: G5.
- No decide el alcance del producto: `QD-005`.

## Pregunta abierta derivada

- `OQ-003` — Postura de cifrado: ¿el operador puede leer el contenido, o solo custodia texto cifrado? (Se resuelve en `QD-004`; se registra acá porque cambia las obligaciones legales de este ADR.)
