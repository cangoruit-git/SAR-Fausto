# PLAN MAESTRO v2 — SISTEMA RELACIONAL (CORREGIDO)

**Documento:** Plano de construcción corregido, posterior a revisión crítica de v1
**Versión:** 2.0
**Estado:** Propuesta — requiere aprobación humana en la Puerta G0
**Reemplaza a:** `PLAN MAESTRO DE CONSTRUCCIÓN DEL SISTEMA RELACIONAL — AGENTE GENTLE-PI + RDD.md` (v1) en lo relativo a **orden, fases, gobernanza y taxonomías**
**Complementa a:** `Especificación Fundamental del Sistema Relacional v1.md` (mantiene su contenido de principios; corrige §39, §62 y §73)
**Regla principal:** NO PROGRAMAR PRODUCTO HASTA QUE LA PUERTA G6 LO AUTORICE. El carril spike (§12) es la única excepción, y requiere autorización explícita.

---

# 0. CÓMO LEER ESTE DOCUMENTO

v1 contiene material valioso: los principios innegociables, la separación autonomía/relación, la distinción experiencia ≠ consecuencia, la cadena impulso → conducta → consecuencia, la baja fricción, la prohibición de scoring global y la regla de no inventar. **Nada de eso se descarta.**

Lo que se corrige es **la forma del plan**: el orden de las fases, la ubicación de las restricciones transversales, el modelo de datos implícito, la ausencia de decisiones fundacionales y la ausencia de un carril de validación temprana. Estos defectos, si no se corrigen, no se manifiestan como errores de documentación: se manifiestan como **daño a personas reales** y como **retrabajo masivo** en la fase de implementación.

Secciones de este documento:

| § | Contenido |
| --- | --- |
| 1 | Registro de hallazgos de la revisión crítica (H-###) |
| 2 | Correcciones estructurales: qué cambia y por qué |
| 3 | Gobernanza documental: jerarquía, autoridad normativa, IDs |
| 4 | Taxonomía epistémica y de evidencia (resuelve la contradicción E1–E5) |
| 5 | Invariantes de privacidad, consentimiento y metadatos |
| 6 | Puertas de seguridad (no "capa posterior") |
| 7 | Modelo de experimentación e inferencia honesta con N=2 |
| 8 | Decisión multicriterio sin scoring |
| 9 | Modelo de amenazas y DPIA |
| 10 | Arquitectura conceptual corregida |
| 11 | Plan de fases corregido: 7 puertas (G0–G6) |
| 12 | Carril paralelo: spike desechable |
| 13 | Protocolo de investigación externa |
| 14 | Testing, verificación y trazabilidad |
| 15 | Definición de "terminado" y criterios de falsación |
| 16 | Bootstrap del repositorio |
| 17 | Decisiones P0 requeridas ahora |
| 18 | Riesgos residuales: por qué este sistema todavía puede fallar |

---

# 1. REGISTRO DE HALLAZGOS DE LA REVISIÓN CRÍTICA

Severidad: **CRITICAL** = si no se corrige, produce daño a personas o invalida el trabajo posterior. **HIGH** = produce retrabajo estructural o conclusiones falsas. **MEDIUM** = deuda de claridad u operativa.

## 1.1 Hallazgos CRITICAL

| ID | Hallazgo | Evidencia | Corrección |
| --- | --- | --- | --- |
| **H-001** | Las dos taxonomías de evidencia son **incompatibles entre sí** y una de ellas mete "hipótesis" como nivel de evidencia. | Plan §8: E1=experimental, E2=meta-análisis, E3=observacional, E4=clínica, E5=testimonio. Spec §39: E1=fuerte, E2=observacional, E3=casos, E4=testimonio, E5=hipótesis. | §4: dos ejes separados (procedencia + evaluación), "hipótesis" fuera de la escalera, "sin evidencia" como valor de primera clase. |
| **H-002** | **Privacidad y consentimiento se definen después** de los modelos que deberían restringir (plan: Fase 12; los modelos van en Fases 2–11). | Plan §49 orden oficial. | §11: privacidad y seguridad pasan a **G1**, antes de toda semántica de dominio. |
| **H-003** | **Seguridad tratada como capa posterior** y sin modelo de amenaza doméstico: no existe el caso "dispositivo compartido con la persona que ejerce control". | Plan §7 "la especificación detallada será posterior"; Spec §45 lista señales pero no dispositivo/rastro. | §6 puertas de seguridad + §9 THR-SHARED-DEVICE. |
| **H-004** | **No existe modelo de amenazas.** En particular, no se contempla *prompt injection* desde el texto del propio usuario para inducir fuga de datos privados o consejo coercitivo. | Ausente en ambos documentos; solo hay "riesgos" genéricos en el plan §12. | §9 modelo de amenazas completo con controles verificables. |
| **H-005** | El **modelo de datos implícito fuerza la reconciliación de reportes contradictorios**: un `Event` con un solo `descripción` y una `fuente` no puede representar dos relatos distintos del mismo hecho sin adjudicar "quién tiene razón". | Spec §20 (Evento con descripción única) + §62; principio "el sistema no debe determinar quién tiene razón". | §5 INV-PRIV-004 + G2: `Event` = ancla temporal; `Observation` = **por informante**, sin verdad única. |
| **H-006** | **Fuga de metadatos no modelada.** La existencia, autoría, tipo y *timestamp* de un registro revelan contenido y conducta ("registró algo a las 23:40 justo después de la pelea"). | Ausente en ambos documentos. | §5 INV-PRIV-003 (los metadatos heredan visibilidad) + §6 G-SAFE-3. |
| **H-007** | El **motor de experimentos no tiene base inferencial**: N=2, sin línea base, sin instrumentos de medida declarados, sin regla de lectura, sin confusores. Produce "aprendizajes" que pueden ser ruido o expectativa presentados como resultado. | Spec §33–§37; plan §21. | §7 modelo de inferencia interna pre-registrada y no causal. |
| **H-008** | El **MVP no es mínimo**: el §66 de la Spec lista 18 capacidades = el sistema completo. Contradice plan §31 ("deliberadamente pequeño") y §65 ("complejidad prematura"). No existe artefacto de alcance ni de **no-objetivos**. | Spec §66 vs plan §31 y §65. | G4 exige `SCOPE.md` con no-objetivos; G6 define un corte vertical delgado. |
| **H-009** | Se asume **una sola verdad compartida**. Falta la regla de render por vista (A / B / compartida) y la regla de **contaminación de datos derivados** (una inferencia compuesta por insumos parcialmente privados no puede compartirse por ser "solo una inferencia"). | Spec §43 solo dice "no presentar como hecho"; plan §6 solo dice "no se comparte automáticamente". | §5 INV-PRIV-002 y INV-PRIV-004. |

## 1.2 Hallazgos HIGH

| ID | Hallazgo | Corrección |
| --- | --- | --- |
| **H-010** | **Waterfall de conocimiento**: prohibir todo código hasta la Fase 14 retrasa justo el aprendizaje barato (¿es usable? ¿es seguro? ¿lo usarían?) que puede invalidar el concepto completo. | §12 carril spike desechable autorizado. |
| **H-011** | **Faltan decisiones fundacionales P0**: dispositivo/cuenta, local vs nube, flujo de datos al LLM, alcance (mantenimiento/formación/individual), piloto. Sin ellas, los modelos de G2–G3 se diseñan sobre supuestos contradictorios. | §17 tabla de decisiones P0 en G0. |
| **H-012** | **Dos órdenes canónicos contradictorios**: plan §49 (evidencia en Fase 8; datos en Fase 15) vs Spec §73 (DATA_MODEL primero; `EVIDENCE_SYSTEM` casi al final). Además, sin mapeo entre `docs/` y OpenSpec/SDD → duplicación garantizada. | §3 jerarquía + §11 único orden; regla: los docs son fuente, los cambios SDD referencian. |
| **H-013** | **Sin glosario ni lenguaje ubicuo**: Observation / Event / experiencia / interpretación / inferencia / hipótesis / patrón / señal se solapan y cada fase puede fijar un sentido distinto. | G0 exige `GLOSSARY.md` normativo y congelado por puerta. |
| **H-014** | **No existe registro de decisiones ni de preguntas abiertas.** La propia regla de cierre de fase (plan §36: "contradicciones + preguntas abiertas registradas") es **inverificable**: no hay dónde. | §3 `docs/adr/` + `docs/OPEN_QUESTIONS.md` como artefactos de primera clase. |
| **H-015** | **Anclaje del LLM en generación de hipótesis**: nada impide que la primera hipótesis generada se convierta en el marco de todas las siguientes y en el marco de las preguntas que se le hacen al usuario (sesgo del entrevistador). | §7 + G3: generación en lote, alternativas obligatorias, orden ciego, atribución visible, lint determinista de lenguaje. |
| **H-016** | No se prohíbe que el modelo **cite literatura desde sus pesos** → alucinación de fuentes en el corazón del "evidence engine". | §13: la evidencia se recupera del almacén curado por ID; sin recuperación, la respuesta es "sin evidencia". |
| **H-017** | Sin estrategia de búsqueda, sin instrumento de evaluación (CASP/GRADE-lite/AMSTAR), sin política de derechos/licencias, sin regla de "evidencia ausente". | §13. |
| **H-018** | Se prohíbe el scoring (§4.3) pero **no se define cómo comparar estrategias**. En la práctica, el implementador inventará un número y violará el principio. | §8 matriz multicriterio sin agregación, pesos en manos humanas. |
| **H-019** | **Ciclo de vida de hipótesis indefinido**: sin estados, sin decaimiento, sin autoría, sin atribución. Una hipótesis "respaldada" con N=2 puede terminar leída como hecho. | §7 estados + atribución obligatoria. |
| **H-020** | **Consentimiento insuficiente**: no hay revocación, ni estatus de lo ya expuesto, ni regla sobre qué significa un "no", ni distinción entre consentimiento de producto y consentimiento de investigación. | §5 INV-PRIV-006/007 + G4 reglas. |
| **H-021** | **Sin DPIA ni ética de piloto**. Sin retención, borrado verificable, portabilidad ni derecho de salida. Recolectar interacción íntima de parejas reales exige más que consentimiento de producto. | §9 + G1 (DPIA-lite) y G4 (retención, export, borrado). |
| **H-022** | **Observabilidad vs privacidad**: logs, trazas y analítica de contenido íntimo no regulados; dependencia de terceros. | §5 INV-PRIV-005 + §9. |
| **H-023** | **Sin requisitos no funcionales**: offline, latencia, costo por LLM, disponibilidad, accesibilidad, idioma, batería. | G4 `NFR.md`. |
| **H-024** | **Testing ausente donde más importa**: invariantes de privacidad ejecutables, golden set de extracción/hipótesis, adversariales de inyección, test de "nada de contenido en logs". | §14 (reutiliza el patrón de *architecture tests* del proyecto SMAT del mismo autor: los invariantes deben ser tests, no prosa). |
| **H-025** | **Ownership y ciclo de vida indefinidos**: ¿quién borra la relación? ¿qué pasa con lo compartido cuando uno se va? ¿quién invita, quién revoca? ¿edad mínima? | G4 `OWNERSHIP.md` + reglas `BR-OWN-###`. |
| **H-026** | **Voz/audio**: se proponen notas de voz (biometría-adyacente) sin política de retención, transcripción ni proveedor. | G4 política de medios. |
| **H-027** | **Sin criterios de falsación** pese a que §69 declara la hipótesis central como hipótesis a validar. Una hipótesis sin criterio de muerte es decorativa. | §15 kill criteria. |
| **H-028** | **Carga de revisión humana descontrolada**: 21 fases con checkpoints y ~20 documentos, sin presupuesto de revisión. Contradice el principio de proteger al revisor. | §11: 7 puertas con presupuesto de revisión declarado. |

## 1.3 Hallazgos MEDIUM

| ID | Hallazgo | Corrección |
| --- | --- | --- |
| **H-029** | Duplicación normativa entre los dos documentos (~60–70% de solapamiento) sin regla de precedencia. Ya divergen (H-001, H-012). | §3: un dueño normativo por tema. |
| **H-030** | `ModelVersion` y `AuditEntry` listados sin semántica (¿versión de qué?). | G5 los define o los elimina. |
| **H-031** | Esquema de IDs solo para `REQ` y `BR`. | §3 esquema completo. |
| **H-032** | Versionado y supersesión de documentos sin mecanismo: no se sabe dónde vive el estado "aprobado". | §3 + `PROJECT_STATUS.md`. |
| **H-033** | `Impulse` sin regla de autoría: riesgo de presentar como dato algo inferido por el sistema. | §5 INV-PRIV-009: lo inferido vive en `Hypothesis`, nunca en `Event`. |
| **H-034** | `Patrón` sin umbral operativo ("múltiples eventos" no es criterio). | G2 define regla de recurrencia mínima y de decaimiento. |
| **H-035** | Sin política de memoria del agente: datos personales podrían terminar en Engram fuera del modelo de privacidad del producto. | §16: en memoria solo decisiones de proyecto, nunca datos de personas. |
| **H-036** | Producto sin nombre, licencia, idioma declarado, ni identidad de repo ("SAR" no está definido en ningún documento). | §16 bootstrap. |
| **H-037** | Escalado de decisiones del agente sin triaje: cada duda interrumpe al humano. | §3 triaje P0/P1/P2 y batching por puerta. |
| **H-038** | "No implementar" genérico sin previsión de spikes. | §12 marco de autorización acotada. |
| **H-039** | La Fase 0 asume un repositorio con stack, tests y convenciones existentes. El repositorio real contiene **dos archivos .md y `.atl/`**: sin git, sin código, sin docs/, sin tests, sin OpenSpec, sin `.pi`. | §16 fase de bootstrap explícita. |
| **H-040** | Sin pre-registro de las preguntas de investigación del propio proyecto. | §13. |

---

# 2. CORRECCIONES ESTRUCTURALES

1. **Las restricciones transversales se mueven al principio.** Privacidad, consentimiento, seguridad, metadatos y modelo de amenazas son *restricciones que atraviesan todos los modelos*, no fases al final. Diseñar el modelo de persona antes de definir la visibilidad obliga a re-tocar cada entidad después.
2. **Una sola jerarquía documental y un solo dueño normativo por tema.** Se elimina la duplicación que ya produjo H-001 y H-012.
3. **Decisiones fundacionales primero.** Ningún modelo de dominio se escribe sobre supuestos no decididos (§17).
4. **Un solo orden canónico**, y las fases se agrupan en 7 puertas con presupuesto de revisión explícito.
5. **Semántica epistémica formal desde el día uno** (dos ejes, "sin evidencia" de primera clase, hipótesis fuera de la escalera de evidencia).
6. **El modelo de datos se corrige antes de escribirlo**: reportes contradictorios, render por vista, contaminación de derivados, metadatos, autoría.
7. **Se introduce un carril de spikes desechables** para comprar el aprendizaje barato que puede invalidar el concepto.
8. **Se formaliza la inferencia interna** (pre-registro, línea base, bandas, prohibición de lenguaje causal) porque el producto *es* un generador de conclusiones sobre personas.
9. **Se define cómo comparar sin puntuar** (§8), para que la prohibición del scoring sea implementable y no decorativa.
10. **Todo invariante crítico es un test ejecutable** (§14), no un párrafo.

---

# 3. GOBERNANZA DOCUMENTAL

## 3.1 Jerarquía y autoridad normativa

| Nivel | Documento | Autoridad sobre | Mutabilidad |
| --- | --- | --- | --- |
| N0 | `CONSTITUTION.md` (derivado de Spec §1–§8, §60, §61, §71 + plan §4) | Principios, invariantes, prohibiciones | Muy baja — requiere decisión humana P0 y nueva versión mayor |
| N1 | `SPEC.md` (la Spec v1 revisada) | Semántica del dominio, entidades, reglas conceptuales | Media — por ADR |
| N2 | `PLAN.md` (este documento) | Proceso, fases, puertas, entregables, gobernanza | Media — por ADR |
| N3 | `docs/adr/ADR-####.md` | Decisiones concretas, con contexto y alternativas | Alta — append-only, supersesión explícita |
| N4 | `openspec/changes/*` (SDD) | Cómo se implementa y verifica un incremento | Alta |
| N5 | `PROJECT_STATUS.md` | Estado vivo y evidencia de aprobación | Vivo |

**Regla de no duplicación:** ningún enunciado normativo puede vivir en dos niveles. Si aparece en dos, uno **referencia** al otro. Toda contradicción detectada se resuelve por ADR, no por edición silenciosa.

## 3.2 Esquema de identificadores

| Prefijo | Artefacto |
| --- | --- |
| `PRIN-###` | Principio constitucional |
| `INV-###` | Invariante de dominio/arquitectura |
| `INV-PRIV-###` | Invariante de privacidad (ejecutable) |
| `BR-###` | Regla de negocio |
| `REQ-###` / `NFR-###` | Requisito funcional / no funcional |
| `DEC-####` | Decisión (ADR) |
| `OQ-###` | Pregunta abierta |
| `H-###` | Hallazgo de revisión |
| `RISK-###` / `THR-###` | Riesgo / amenaza |
| `SRC-###` / `CLM-###` / `EVD-###` | Fuente / afirmación / registro de evidencia |
| `EVT-###` / `OBS-###` / `INT-###` | Evento / observación / interpretación |
| `PAT-###` / `HYP-###` | Patrón / hipótesis |
| `STR-###` / `EXP-###` / `OUT-###` | Estrategia / experimento / resultado |
| `QD-###` | Pregunta de decisión escalada al humano |

## 3.3 Triaje de decisiones (corrige H-037)

- **P0 (bloqueante):** detiene la puerta. Requiere decisión humana antes de continuar. Se presenta con el formato de la Spec §37.
- **P1 (diferible):** se registra como `OQ-###` con fecha límite = la puerta indicada, y se continúa con una **opción por defecto conservadora** documentada.
- **P2 (informativa):** se registra y se resuelve en el cierre de puerta.

**Batching:** las decisiones P1 y P2 no interrumpen; se entregan juntas al cierre de puerta. Solo P0 interrumpe.

---

# 4. TAXONOMÍA EPISTÉMICA Y DE EVIDENCIA (corrige H-001)

Se separan **cuatro ejes independientes**. Mezclarlos fue el error de v1 §8 y Spec §39.

## 4.1 Eje A — Naturaleza epistémica del enunciado

| Código | Significado | Regla |
| --- | --- | --- |
| `REG` | Hecho registrado (lo que el sistema observó directamente: timestamps, acciones en la app) | Dato, no interpretación |
| `DEC` | Declaración de una persona ("me sentí ignorada") | Es verdad sobre la experiencia, no sobre el mundo |
| `INT` | Interpretación de una persona sobre un evento | Siempre atribuida a quien la hizo |
| `INF` | Inferencia del sistema | Nunca presentable como hecho; siempre con proveniencia |
| `HYP` | Hipótesis | **Nunca es evidencia.** Es una afirmación a contrastar |
| `EXT` | Enunciado proveniente de una fuente externa | Requiere `SRC-###` con appraisal |
| `UNK` | Desconocido / información insuficiente | Valor legítimo y frecuente; prohibido rellenarlo |

**Regla dura:** `HYP` no puede aparecer en ningún campo tipado como evidencia. (Esto invalida Spec §39, donde "hipótesis" era E5.)

## 4.2 Eje B — Afirmante

`A` · `B` · `AMBOS` · `SISTEMA` · `EXTERNO`.

Todo enunciado lleva afirmante. Un enunciado derivado por el sistema y "confirmado" por A sigue siendo `INF` con afirmante `SISTEMA` más una `DEC` de A; **no se fusionan**.

## 4.3 Eje C — Clase de procedencia (solo para `EXT`)

| Código | Procedencia |
| --- | --- |
| `S1` | Estudio experimental controlado |
| `S2` | Síntesis sistemática (revisión sistemática, meta-análisis) |
| `S3` | Estudio observacional (cohorte, caso-control, transversal) |
| `S4` | Documentación clínica o profesional revisada |
| `S5` | Testimonio o experiencia individual |

`S1`–`S5` es **procedencia, no calidad**. Un `S5` puede ser la única información disponible sobre un fenómeno y sigue siendo `S5`.

## 4.4 Eje D — Evaluación (appraisal) para `EXT`

- Instrumento declarado (CASP por diseño, AMSTAR-2 para síntesis, GRADE-lite para certeza).
- Campos obligatorios: `diseño`, `población`, `n`, `contexto`, `resultado`, `limitaciones`, `riesgo_de_sesgo`, `aplicabilidad`, `fecha`, `idioma`, `derechos_de_uso`, `revisor`, `fecha_de_appraisal`, `fecha_de_re_verificación`.
- Estados: `EVALUADA` · `NO_EVALUADA` · `CONTESTADA`.

## 4.5 Ausencia de evidencia (corrige H-016/H-017)

**`NO_EVIDENCE_RETRIEVED` es un valor de primera clase.** Reglas:

1. El sistema **no puede** presentar conocimiento de los pesos del modelo como evidencia. Sin `SRC-###` en el almacén curado, la respuesta es "no se recuperó evidencia".
2. Toda cita debe resolver a un `SRC-###` con URL/DOI y fragmento almacenado (verificable).
3. Es una **falla bloqueante** (no un warning) que una respuesta genere bibliografía no presente en el almacén.

## 4.6 Regla de lenguaje (corrige H-015)

Lint determinista sobre toda salida del LLM. Prohibido y bloqueado:

- diagnóstico o etiqueta clínica sobre una persona;
- lenguaje causal ("esto causó", "porque vos");
- certeza ("es claro que", "siempre", "nunca");
- veredicto sobre la relación o sobre quién tiene razón;
- instrucción prescriptiva ("tenés que");
- cualquier frase que permita citar al sistema como árbitro ("el sistema dice que vos…"). La redacción es siempre en primera persona sugerida, atribuida y revocable por la persona.

---

# 5. INVARIANTES DE PRIVACIDAD, CONSENTIMIENTO Y METADATOS (corrige H-002, H-005, H-006, H-009, H-020)

Estos invariantes se definen **antes** de los modelos de dominio, porque los restringen. Cada uno debe tener un test ejecutable (§14).

| ID | Invariante |
| --- | --- |
| `INV-PRIV-001` | Ningún dato con visibilidad `PRIVATE_A` es legible por B en **ninguna** superficie: API, vista renderizada, export, log, traza, telemetría, notificación, prompt enviado a un tercero. |
| `INV-PRIV-002` | Todo artefacto derivado declara `provenance[]` con los IDs de sus insumos. La visibilidad máxima de un derivado es la **intersección** de la visibilidad de sus insumos. Un derivado con cualquier insumo privado no es compartible por defecto. |
| `INV-PRIV-003` | **Los metadatos heredan la visibilidad del dato**: existencia, autoría, tipo, `occurred_at`, `recorded_at`, frecuencia y "estado de actividad". No existe "solo metadatos" compartido por defecto. |
| `INV-PRIV-004` | **No existe una vista compartida almacenada.** Todo se renderiza por vista (`view(A)`, `view(B)`, `view(shared)`). No hay "verdad única" ni campo único de descripción de evento. |
| `INV-PRIV-005` | Ningún contenido íntimo cruza a logs, trazas, analítica de terceros, *crash reports* ni memoria del agente. Los logs referencian IDs, nunca contenido. |
| `INV-PRIV-006` | La revocación de consentimiento detiene la visibilidad **futura**. Lo ya expuesto se marca `EXPOSED` (no se puede des-ver) y los derivados que dependían de ese dato se marcan para revisión o retiro. |
| `INV-PRIV-007` | El **rechazo** a un experimento es información sobre el rechazo, no sobre el motivo. El sistema no infiere ni muestra el motivo del rechazo. |
| `INV-PRIV-008` | Existen export completo y borrado verificable (incluidos derivados) en un plazo declarado, con evidencia de ejecución. |
| `INV-PRIV-009` | `Impulse`, `Emotion` e `Interpretation` **solo** pueden existir como declaración de persona. Si el sistema los infiere, viven como `HYP` y nunca aparecen dentro del evento como dato. (Corrige H-033.) |
| `INV-PRIV-010` | El contexto entregado al LLM se compone **por vista del solicitante**. Un pedido de A nunca incluye datos privados de B, ni siquiera como resumen, embedding o "contexto derivado". |

## 5.1 Consentimiento: modelo mínimo

- **Alcance** (`ConsentScope`): qué dato, para qué uso (ver, derivar, compartir, experimentar, investigar), por cuánto tiempo.
- **Granularidad:** por dato o por categoría; nunca "acepto todo" como único camino.
- **Asimetría:** A no puede consentir en nombre de B.
- **Efectos:** el modelo distingue *aceptar*, *rechazar*, *no respondido* y *retirado*. **"No respondido" nunca equivale a aceptado.**
- **Investigación ≠ producto:** el uso de datos de un piloto para aprender sobre el producto requiere consentimiento separado, revocable, y con datos minimizados.

---

# 6. PUERTAS DE SEGURIDAD (corrige H-003)

La seguridad no es una capa del final del pipeline: es una **serie de puertas que pueden detener el pipeline**. Se define en G1, antes de estrategias y experimentos.

| ID | Puerta | Comportamiento |
| --- | --- | --- |
| `G-SAFE-0` | Entrada al producto | Declaración de límites (no es terapia, no es servicio de emergencia) + recursos de ayuda humana por jurisdicción. |
| `G-SAFE-1` | Detección de señales | Clasificador conservador sobre violencia, amenaza, coerción, control, aislamiento, miedo, abuso. Ante señal: **no se generan estrategias de negociación ni de "punto medio"**. Se ofrece orientación a ayuda humana. Se presenta como **señal**, nunca como conclusión. |
| `G-SAFE-2` | Veto independiente del consentimiento | Aunque ambos consientan, no se propone un experimento con señales activas o crisis aguda. El consentimiento no habilita daño. |
| `G-SAFE-3` | Modo dispositivo compartido | Sin notificaciones con contenido, sin rastro en pantallas recientes, bloqueo rápido, y posibilidad de operar sin dejar historial visible para la otra persona. Debe asumirse **por defecto hasta que el usuario elija lo contrario**. |
| `G-SAFE-4` | Asimetría de errores declarada | Falso negativo (no detectar) y falso positivo (etiquetar de más) tienen costos distintos; ambos se miden y ambos tienen umbral de tolerancia explícito. |
| `G-SAFE-5` | No evidencia en contra | El sistema declara que los datos no son prueba y que pueden ser accedidos por terceros (dispositivo compartido, proceso legal). |
| `G-SAFE-6` | Edad | Edad mínima declarada; menores excluidos; si se detecta, detener. |

**Regla dura:** ninguna estrategia ni experimento se propone sin haber atravesado `G-SAFE-1` y `G-SAFE-2`, con resultado registrado.

---

# 7. MODELO DE EXPERIMENTACIÓN E INFERENCIA HONESTA (corrige H-007, H-019)

## 7.1 Instrumentos y medidas

Toda métrica debe declarar: `instrumento`, `escala`, `quién_reporta`, `cadencia`, `ventana`, `dirección_esperada`, `banda_de_sin_cambio`, `señales_de_daño`.

Sin instrumento declarado, la métrica no existe. No se aceptan métricas ad-hoc creadas después de ver el resultado.

## 7.2 Pre-registro

Antes de iniciar un experimento se congelan: hipótesis, estrategia, indicadores, dirección esperada, banda de "sin cambio", señales de daño, duración y condiciones de cancelación. **No se modifica el pre-registro después de observar datos**, salvo registrar la modificación y reiniciar el conteo.

## 7.3 Línea base

Periodo previo sin intervención, con al menos K mediciones del mismo instrumento. Sin línea base, el resultado es `NO_CONCLUYENTE_INTERNO` por construcción.

## 7.4 Regla de lectura

El sistema puede reportar únicamente:

1. dirección del cambio (mejor/igual/peor) por indicador y por persona;
2. si el valor **sale de la banda de variación** de la línea base;
3. **acuerdo o desacuerdo** entre A y B (esto es un hallazgo en sí mismo, no un error);
4. señales de daño;
5. confusores presentes.

El sistema **no puede** reportar: "funcionó", "causó", "probado", "significativo", valores p, tamaños de efecto, comparaciones con otras parejas ni generalizaciones. **Confusores declarados obligatoriamente**: expectativa/placebo, demanda (complacer al sistema), evento externo, regresión a la media, desgaste del registro.

## 7.5 Ciclo de vida de hipótesis (corrige H-019)

`PROPUESTA` → `EN_OBSERVACION` → `RESPALDADA_DEBIL` · `CONTRADICHA` · `NO_CONCLUYENTE` · `ABANDONADA` · `VENCIDA`

- Autoría obligatoria y visible (`A` · `B` · `SISTEMA` · `CONJUNTA`).
- Decaimiento por tiempo sin observaciones nuevas.
- Revisión obligatoria al cambiar de contexto.
- **Ningún estado equivale a hecho.** `RESPALDADA_DEBIL` con N=2 sigue siendo hipótesis.

## 7.6 Anti-anclaje en generación de hipótesis (corrige H-015)

1. Se generan **en lote** (mínimo 3), no una.
2. Se presentan en **orden ciego** y con la explicación alternativa explícita.
3. Ninguna hipótesis del sistema puede condicionar las preguntas siguientes sin declararlo.
4. Las hipótesis del sistema y las de las personas se muestran con autoría distinta y las personas pueden **rechazarlas** con una acción de primera clase (y el rechazo se conserva).
5. Toda hipótesis declara: evidencia utilizada (IDs), explicaciones alternativas, nivel de confianza, y **cómo podría refutarse**.

## 7.7 Efecto observador como hipótesis, no como beneficio

Registrar la relación la modifica. Esto no es un efecto secundario: es parte de la intervención. Debe tratarse como `HYP` explícita y medirse (reactividad, moral licensing, "actuar para el registro"), no asumirse como mejora.

---

# 8. DECISIÓN MULTICRITERIO SIN SCORING (corrige H-018)

## 8.1 Formato obligatorio de evaluación de estrategia

Matriz `perspectiva × horizonte`, con celdas que contienen: `beneficio/coste esperado` (ordinal explícito), `confianza` (baja/media/alta), `fuente del juicio` (`DEC_A`, `DEC_B`, `INF_SISTEMA`, `EXT`).

| | Corto | Medio | Largo |
| --- | --- | --- | --- |
| **A** | … | … | … |
| **B** | … | … | … |
| **Relación** | … | … | … |

## 8.2 Reglas

1. **Prohibida la agregación automática en un escalar.** El sistema no produce un número único.
2. Las **ponderaciones las fijan las personas** y se declaran; el sistema nunca las inventa ni las oculta.
3. El sistema puede mostrar el **conjunto no dominado** (frontera de Pareto) y los conflictos; no "el ganador".
4. Si el sistema ordena para mostrar, debe declarar el criterio y permitir cambiarlo.
5. Si la única configuración posible **viola un límite declarado**, el sistema lo dice y **no la presenta como opción**.
6. Toda estrategia declara evidencia (`SRC-###`/`CLM-###`) o `NO_EVIDENCE_RETRIEVED`.

---

# 9. MODELO DE AMENAZAS Y DPIA (corrige H-004, H-021, H-022)

## 9.1 Activos

Contenido íntimo · existencia del uso · metadatos temporales y de frecuencia · datos derivados · identidad · credenciales · integridad del almacén de evidencia.

## 9.2 Adversarios

| ID | Adversario |
| --- | --- |
| `THR-PARTNER` | La otra persona de la relación, en conflicto |
| `THR-EXPARTNER` | Ex pareja con conocimiento del sistema |
| `THR-HOUSEHOLD` | Terceros en el hogar (familia, visitas) |
| `THR-DEVICE` | Acceso físico al dispositivo desbloqueado |
| `THR-CLOUD` | Proveedor de nube/LLM (retención, entrenamiento, fuga) |
| `THR-LEGAL` | Requerimiento legal / acceso por proceso |
| `THR-SUPPLY` | Compromiso de dependencia o de cadena de suministro |
| `THR-INJECT` | Inyección de instrucciones mediante el texto del propio usuario |
| `THR-SYSTEM` | El propio sistema produciendo consejo dañino |

## 9.3 Vectores y controles mínimos

| Vector | Control | Verificación |
| --- | --- | --- |
| Dispositivo compartido | `G-SAFE-3`; visibilidad por vista; sin notificaciones con contenido | Test de UI + test de política de notificación |
| Metadatos | `INV-PRIV-003` | Test de superficie de metadatos |
| Notificaciones / preview | Texto neutro fijo; opción de ocultar | Test de plantillas |
| Caché, backups, export | Cifrado, exclusión de caché de contenido íntimo, export bajo demanda | Test de artefactos generados |
| Logs y telemetría | `INV-PRIV-005`; solo IDs | Test que falla si aparece contenido |
| Prompt injection | `INV-PRIV-010`; composición por vista; el modelo no decide visibilidad; validación determinista de salida | Suite adversarial (A intenta fugarse datos de B y viceversa) |
| Memoria de agente (Engram) | Sin datos de personas; solo decisiones de proyecto | Revisión de política + test de no-escritura |
| Proveedor LLM | Contrato sin entrenamiento, retención cero si es posible, o modelo local | Registro de decisión `DEC-####` |
| Consejo dañino | Lint de lenguaje + `G-SAFE-1/2` | Suite de casos adversarios |
| Proceso legal | Declaración explícita (`G-SAFE-5`) + minimización | Documento de transparencia |

## 9.4 DPIA

`DPIA-lite.md` obligatoria **antes de cualquier piloto con personas reales**: finalidad, base legal, categorías de datos (incluye categoría especial: vida sexual/salud), minimización, retención, encargados, transferencias, derechos, riesgos, medidas, y criterio de no-arranque si el riesgo residual es inaceptable.

---

# 10. ARQUITECTURA CONCEPTUAL CORREGIDA

Diferencia clave con v1: **las restricciones no son una etapa posterior, son puertas**.

```text
                    POLÍTICA (G1)
        privacidad · consentimiento · seguridad · lenguaje
                            │
   ┌────────────────────────┼────────────────────────┐
   ▼                        ▼                        ▼
PERSONA A               RELACIÓN                PERSONA B
(privado A)                                       (privado B)
   │                        │                        │
   └───────────┬────────────┴───────────┬────────────
               ▼                        ▼
        EVENTOS (ancla)          OBSERVACIONES por informante
               │                        │   (sin verdad única)
               └───────────┬────────────
                           ▼
                  PATRONES POTENCIALES
                           ▼
                     HIPÓTESIS
               (con alternativas + autoría)
                           │
              ┌────────────────────────┐
              ▼                         ▼
     EVIDENCIA EXTERNA            INCERTIDUMBRE
     (almacén curado,             (NO_EVIDENCE,
      por ID, con appraisal)       NO_CONCLUYENTE)
              ────────────┬────────────┘
                           ▼
                      ESTRATEGIAS
                 (matriz multicriterio,
                  sin agregación)
                           │
                           ▼
              ┌──── G-SAFE-1 / G-SAFE-2 ────┐  ← PUERTA
              │  (puede detener aquí)       │
              └────────────┬────────────────┘
                           ▼
                  CONSENTIMIENTO EXPLÍCITO
                  de cada participante afectado
                           ▼
                     EXPERIMENTO
                  (pre-registrado, con
                   línea base y daño)
                           ▼
                      RESULTADOS
              (dirección, banda, acuerdo,
               daño, confusores — nunca causa)
                           ▼
                ACTUALIZACIÓN DE HIPÓTESIS
                 (nunca a "hecho")
                           ▼
                  RENDER POR VISTA
              view(A) · view(B) · view(shared)
```

**Nodo faltante que v1 no tenía:** `RENDER POR VISTA` al final. Sin él, `INV-PRIV-004` no es implementable.

---

# 11. PLAN DE FASES CORREGIDO: 7 PUERTAS

Presupuesto de revisión: **≤ 3 documentos y ≤ 60 minutos de lectura humana por puerta** (corrige H-028). Si una puerta excede eso, se parte.

## G0 — AUTORIDAD, ALCANCE Y BOOTSTRAP

**Objetivo:** fijar el terreno antes de pensar el dominio.

**Entregables**

- `README.md`, `LICENSE`, `PROJECT_STATUS.md`
- `docs/00-GOVERNANCE.md` (jerarquía, IDs, triaje)
- `docs/adr/ADR-0001..ADR-000n` (decisiones P0, §17)
- `docs/SCOPE.md` (alcance + **no-objetivos** explícitos)
- `docs/GLOSSARY.md` (lenguaje ubicuo v0)
- `docs/OPEN_QUESTIONS.md`
- `docs/REVIEW_FINDINGS.md` (este §1, versionado)
- Estructura de carpetas mínima (§16)

**Criterio de salida:** decisiones P0 resueltas y registradas; no-objetivos escritos; glosario v0 aceptado; repositorio inicializado.

**Absorbe:** v1 Fase 0 y Fase 1.

---

## G1 — CONSTITUCIÓN, PRIVACIDAD Y SEGURIDAD

**Objetivo:** definir las restricciones transversales **antes** de la semántica.

**Entregables**

- `docs/CONSTITUTION.md` (principios, `PRIN-###`, `INV-###`)
- `docs/privacy/PRIVACY_MODEL.md` (`INV-PRIV-001..010`, consentimiento, ownership, retención, export, borrado)
- `docs/privacy/DPIA-lite.md`
- `docs/safety/SAFETY_MODEL.md` (`G-SAFE-0..6`, señales, escalado, recursos)
- `docs/security/THREAT_MODEL.md` (§9)
- Taxonomía epistémica (`docs/EPISTEMICS.md`, §4)

**Criterio de salida:** todo invariante de privacidad tiene una estrategia de test declarada; toda amenaza tiene control y método de verificación; ninguna puerta de seguridad queda indefinida.

**Movimiento respecto a v1:** Fases 12 y 13 se adelantan de la posición 12–13 a G1.

---

## G2 — SEMÁNTICA DEL DOMINIO

**Objetivo:** definir qué representa cada cosa, con las restricciones ya fijadas.

**Entregables**

- `docs/domain/PERSON_MODEL.md` (persona, identidad, valores, objetivos, necesidades, preferencias, límites, hábitos)
- `docs/domain/RELATIONSHIP_MODEL.md` (relación, membresía, objetivos compartidos, acuerdos, conflictos)
- `docs/domain/EVENT_MODEL.md` (evento como ancla; **observación por informante**; `occurred_at` vs `recorded_at`)
- `docs/domain/EXPERIENCE_MODEL.md` (emoción, interpretación, impulso, conducta, consecuencia, resultado inmediato/posterior)
- `docs/domain/PATTERN_MODEL.md` (recurrencia mínima, decaimiento, contexto, excepciones)
- `docs/domain/HYPOTHESIS_MODEL.md` (estados, autoría, alternativas, refutación)
- `docs/domain/TEMPORAL_MEMORY.md` (recencia, repetición, duración, cambio, versionado del perfil)
- `docs/domain/COGNITIVE_MECHANISMS.md` (catálogo **finito y cerrado** inicial; cada uno con definición, señales, explicaciones alternativas, falsos positivos, fuentes, y qué **no** permite concluir)
- `docs/MEASUREMENT.md` (instrumentos, escalas, cadencia, bandas)

**Criterio de salida:** cada concepto declara significado, qué **no** representa, autoría, visibilidad, temporalidad, mutabilidad, y su relación con `INV-PRIV-*`. El glosario se eleva a v1 congelado.

**Absorbe:** v1 Fases 2, 3, 4, 5, 6, 7, 11.

---

## G3 — CONOCIMIENTO, ESTRATEGIAS Y EXPERIMENTOS

**Objetivo:** el motor de razonamiento del sistema.

**Entregables**

- `docs/evidence/EVIDENCE_MODEL.md` (`SRC`/`CLM`/`EVD`, ejes C y D)
- `docs/evidence/EVIDENCE_POLICY.md` (fuentes admitidas, appraisal, re-verificación, derechos, `NO_EVIDENCE_RETRIEVED`)
- `docs/evidence/SEARCH_PROTOCOL.md` (bases, consultas, inclusión/exclusión, PRISMA-lite, pre-registro)
- `docs/domain/STRATEGY_MODEL.md` (multicriterio sin scoring, §8)
- `docs/domain/EXPERIMENT_MODEL.md` (pre-registro, línea base, lectura, daño, cancelación)
- `docs/domain/INFERENCE_RULES.md` (§7)

**Criterio de salida:** ninguna estrategia puede existir sin evaluación multicriterio y sin declaración de evidencia; ningún experimento puede existir sin pre-registro y línea base.

**Absorbe:** v1 Fases 8, 9, 10.

---

## G4 — REQUISITOS, REGLAS Y NO FUNCIONALES

**Entregables**

- `docs/requirements/SYSTEM_REQUIREMENTS.md` (`REQ-###`, verificables y trazables)
- `docs/requirements/NON_FUNCTIONAL.md` (`NFR-###`: offline, latencia, costo LLM, disponibilidad, accesibilidad, idioma, batería)
- `docs/requirements/BUSINESS_RULES.md` (`BR-###`, incluidos ownership, ciclo de vida, edad, medios/voz, retención, export, borrado)
- `docs/requirements/TRACEABILITY.md` (matriz `PRIN/INV → REQ → BR → test`)

**Criterio de salida:** cada `REQ` traza a al menos un principio o invariante; cada `INV-PRIV-*` traza a al menos un test planificado.

**Absorbe:** v1 Fase 14 y Fase 16.

---

## G5 — DISEÑO TÉCNICO

**Entregables**

- `docs/architecture/DATA_MODEL_V1.md` (entidades, campos, cardinalidades, ownership, visibilidad por campo, proveniencia, lifecycle, índices, auditoría, borrado)
- `docs/architecture/TECHNICAL_ARCHITECTURE_V1.md` (stack, local vs nube ya decidido en G0, despliegue, observabilidad sin contenido)
- `docs/architecture/AI_ARCHITECTURE_V1.md` (roles separados, composición por vista, validación determinista, fallback, presupuesto de costo, degradación)
- `docs/api/API_SPEC_V1.md` (propósito, entrada/salida, autorización, privacidad, errores, idempotencia, trazabilidad, validación)

**Criterio de salida:** el modelo de datos **puede expresar** reportes contradictorios, render por vista, derivados con proveniencia y metadatos con visibilidad. Si no puede, no está terminado.

**Absorbe:** v1 Fases 15, 17, 18, 19.

---

## G6 — MVP E IMPLEMENTACIÓN

**Regla:** un **corte vertical delgado**, no la lista de 18 puntos de Spec §66.

**Corte vertical candidato (un solo camino completo, con la mínima superficie):**
capturar un evento con baja fricción → separar observación de interpretación → ver la propia vista → recibir 3 hipótesis alternativas con autoría → rechazar o aceptar → ver el estado de la hipótesis → borrar/exportar y verificar privacidad.
**Fuera del MVP:** estrategias, experimentos, evidencia externa, voz, formación de relaciones, métricas relacionales.

**Entregables:** cambios SDD (`openspec/changes/…`) que **referencian** los documentos de G1–G5; tests por invariante; verificación independiente; revisión nativa si RDD está habilitado; entrega según política del repositorio.

**Criterio de salida:** los invariantes de privacidad pasan como tests; la suite adversarial de inyección pasa; ninguna superficie filtra contenido.

---

## 11.1 Mapa de migración v1 → v2

| v1 | v2 |
| --- | --- |
| Fase 0 Inspección | **G0** |
| Fase 1 Auditoría del concepto | **§1** (entregada) + **G0** |
| Fases 2, 3, 4, 5, 6, 7, 11 | **G2** |
| Fases 8, 9, 10 | **G3** |
| Fases 12, 13 | **G1** (adelantadas) |
| Fase 14 | **G4** |
| Fase 15, 16, 17, 18, 19 | **G4/G5** |
| Fase 20 MVP | **G6** |

---

# 12. CARRIL PARALELO: SPIKE DESECHABLE (corrige H-010, H-038)

**Problema que resuelve:** v1 prohíbe todo código hasta la Fase 14. Eso deja sin respuesta —durante meses— las preguntas que pueden invalidar el proyecto entero: ¿es usable una captura de baja fricción? ¿se entiende una hipótesis como hipótesis? ¿esto se siente invasivo?

**Autorización acotada (no es implementación de producto):**

| Restricción | Valor |
| --- | --- |
| Datos | **Solo sintéticos o propios del autor.** Prohibido cualquier dato de una relación real de terceros. |
| Persistencia | Ninguna persistencia durable de contenido. Sin base de datos de producción. |
| Código | Desechable. No puede convertirse en código de producto sin pasar por G5+G6. |
| Alcance | Una pregunta de aprendizaje por spike, declarada antes de empezar. |
| Duración | Time-box explícito (p. ej. 2 días de esfuerzo). |
| Salida | `docs/spikes/SPIKE-###.md`: pregunta, qué se probó, qué se aprendió, qué se descarta. |
| Cierre | El código se archiva fuera del árbol de producto o se borra. |
| Autorización | Requiere autorización humana explícita, una vez, con alcance nombrado. |

**Spikes candidatos de mayor valor:**

1. ¿La captura en < 20 segundos es posible sin convertirla en formulario?
2. ¿3 hipótesis alternativas se leen como hipótesis (test de comprensión) o como veredicto?
3. ¿Cómo se siente ver la propia vista sabiendo que la otra persona tiene otra?
4. ¿El lint de lenguaje bloquea las frases dañinas en una suite adversaria?

---

# 13. PROTOCOLO DE INVESTIGACIÓN EXTERNA (corrige H-016, H-017, H-040)

## 13.1 Clases admitidas

| Clase | Contenido | Herramientas |
| --- | --- | --- |
| `documentation` | Documentación oficial de plataformas, librerías, normativa | `fetch_content` |
| `open-web` | Búsqueda, verificación de fuentes y recuperación de contenido original | `web_search`, `source_check`, `fetch_content`, `get_search_content` |

Puertas genéricas MCP no son ruta de evidencia. La disponibilidad se verifica antes de recolectar; si una clase no está disponible, se declara y la puerta correspondiente queda bloqueada.

## 13.2 Disciplina obligatoria

1. **Pre-registro** de las preguntas (`RQ-###`) antes de buscar.
2. Registrar: pregunta, consulta, herramienta, URL/DOI, fecha de recuperación, editor, versión, **fragmento textual**, y el `CLM-###` al que sirve.
3. **Validador de publisher/versión** antes de citar.
4. Un fragmento sin URL resoluble no es evidencia.
5. **Prohibido citar desde los pesos del modelo.** Si el fragmento no está en el almacén, la respuesta es `NO_EVIDENCE_RETRIEVED`.
6. Los niveles `S1`–`S5` (§4.3) se asignan en la recolección, no por el LLM.
7. Derechos de uso: qué se puede almacenar (fragmento/abstract) y qué solo referenciar.

## 13.3 Preguntas de investigación del proyecto (pre-registradas)

`RQ-001` ¿Qué evidencia existe sobre experimentos conductuales autoinformados en parejas y su validez? · `RQ-002` ¿Qué se sabe sobre fricción de autorregistro y adherencia? · `RQ-003` ¿Cómo se presentan hipótesis a personas legas sin inducir certeza? · `RQ-004` ¿Qué se sabe sobre daño de intervenciones digitales de pareja? · `RQ-005` ¿Qué señales de violencia tienen mejor desempeño conocido en detección automatizada y qué falsos positivos producen? · `RQ-006` ¿Qué dice la literatura sobre reactividad del autorregistro? · `RQ-007` ¿Riesgos de escalada en recomendaciones de "punto medio" en relaciones coercitivas?

---

# 14. TESTING, VERIFICACIÓN Y TRAZABILIDAD (corrige H-024)

## 14.1 Los invariantes son tests ejecutables

Reutilizando el patrón que ya funcionó en el proyecto SMAT del mismo autor: **los invariantes viven como tests de arquitectura, no como prosa.**

| Suite | Verifica |
| --- | --- |
| `tests/privacy/` | `INV-PRIV-001` a `010` por frontera (API, render, export, logs, prompts) |
| `tests/architecture/` | Separación de roles del LLM; nadie decide visibilidad fuera del módulo de política; no hay vista compartida almacenada |
| `tests/adversarial/` | Inyección desde texto del usuario (A contra B y B contra A); lenguaje prohibido; conteo de falsos positivos/negativos de seguridad |
| `tests/golden/` | Extracción estructurada y generación de hipótesis contra un conjunto dorado con criterios explícitos |
| `tests/no_content_logs` | Falla si aparece contenido íntimo en cualquier log/traza/telemetría |
| `tests/leak_metadata` | Falla si un metadato privado es visible para el otro |

## 14.2 Verificación

- Quien implementa no es la única fuente de confianza sobre la implementación (plan §42 se mantiene).
- La verificación compara **qué se pidió vs qué se construyó** contra `REQ`/`BR`, no "¿compila?".
- RDD se respeta como infraestructura externa; no se inventan receipts ni hashes; "terminado" ≠ "revisado" (plan §43 se mantiene).

## 14.3 Trazabilidad

`PRIN → INV → REQ → BR → diseño → implementación → test → verificación`, con IDs (§3.2). Todo elemento crítico responde "¿por qué existe esta regla?".

---

# 15. DEFINICIÓN DE "TERMINADO" Y CRITERIOS DE FALSACIÓN

## 15.1 Terminado

Un artefacto está terminado si: objetivo cumplido + decisiones registradas + contradicciones identificadas con ID + preguntas abiertas registradas + dependencias conocidas + trazabilidad (`PRIN/INV → REQ → BR → test`) + visibilidad declarada por campo.

## 15.2 Puerta bloqueada

Una puerta **no se abre** si existe un `OQ-###` P0 sin resolver, un `INV-PRIV-*` sin test planificado, o una amenaza sin control.

## 15.3 Kill criteria del proyecto (corrige H-027)

Criterios de falsación de la hipótesis central (Spec §69). Si se cumple cualquiera, **se detiene y se replantea el producto**:

| ID | Criterio |
| --- | --- |
| `KILL-1` | Tras 4 semanas de uso, menos del X% de las semanas tiene al menos un registro (fracaso de baja fricción). |
| `KILL-2` | Un test de comprensión muestra que las personas leen las hipótesis como veredictos o diagnósticos. |
| `KILL-3` | Ocurre **un** daño identificable atribuible a un consejo del sistema (no se tolera "uno más"). |
| `KILL-4` | No se puede demostrar aislamiento de privacidad a costo razonable. |
| `KILL-5` | El valor percibido no supera al de un diario compartido simple. |
| `KILL-6` | El sistema es usado como arma en conflicto ("el sistema dice que vos…") en más de una fracción declarada de los casos observados. |

---

# 16. BOOTSTRAP DEL REPOSITORIO (corrige H-035, H-036, H-039)

Estado real verificado: el repositorio contiene **dos documentos `.md`** y `.atl/` (estado de runtime de Pi, ya ignorado). **No hay git, código, `docs/`, tests, OpenSpec ni configuración `.pi`.** La Fase 0 de v1 era inejecutable tal como estaba escrita.

## 16.1 Estructura inicial mínima

```text
README.md
LICENSE
PROJECT_STATUS.md
.gitignore                       (existe: ignora .atl/)
PLAN_MAESTRO_v2_CORREGIDO.md     (este documento)
Especificación Fundamental del Sistema Relacional v1.md
PLAN MAESTRO DE CONSTRUCCIÓN … (v1, conservado como histórico)

docs/
  00-GOVERNANCE.md
  SCOPE.md
  GLOSSARY.md
  EPISTEMICS.md
  OPEN_QUESTIONS.md
  MEASUREMENT.md
  REVIEW_FINDINGS.md
  adr/            ADR-0001..n
  privacy/        PRIVACY_MODEL.md, DPIA-lite.md
  safety/         SAFETY_MODEL.md
  security/       THREAT_MODEL.md
  domain/         PERSON_MODEL.md, RELATIONSHIP_MODEL.md, …
  evidence/       EVIDENCE_MODEL.md, EVIDENCE_POLICY.md, SEARCH_PROTOCOL.md
  requirements/   SYSTEM_REQUIREMENTS.md, NON_FUNCTIONAL.md, BUSINESS_RULES.md, TRACEABILITY.md
  architecture/   DATA_MODEL_V1.md, TECHNICAL_ARCHITECTURE_V1.md, AI_ARCHITECTURE_V1.md
  api/            API_SPEC_V1.md
  spikes/         SPIKE-###.md
openspec/          (solo cuando SDD se active en G5/G6)
```

**Regla:** **no crear archivos vacíos.** Cada archivo nace con contenido en la puerta que lo produce.

## 16.2 Política de idioma

Existe convención no-inglesa en el proyecto (los documentos fundacionales están en español). Por tanto **los artefactos del proyecto se escriben en español**, con identificadores, nombres de archivo de código, nombres de entidades y mensajes de commit en inglés cuando sean código (convención técnica estándar). La conversación con el usuario es en español rioplatense.

## 16.3 Política de memoria del agente

Engram almacena **decisiones, hallazgos, patrones y estado de proyecto**. **Nunca** contenido íntimo, datos de participantes, ni transcripciones. `INV-PRIV-005` aplica también al agente.

## 16.4 Identidad del repositorio

Pendiente de decisión (`QD-001`): nombre del producto, definición de "SAR", licencia y visibilidad del repositorio.

---

# 17. DECISIONES P0 REQUERIDAS AHORA

Estas decisiones **determinan la arquitectura** y no pueden diferirse sin diseñar sobre supuestos contradictorios.

| ID | Decisión | Opciones | Consecuencia principal | Reversibilidad |
| --- | --- | --- | --- | --- |
| `QD-001` | Identidad: nombre, significado de "SAR", licencia, visibilidad del repo | (a) definir ahora · (b) provisional y revisar en G4 | Identidad pública, obligaciones de licencia | Fácil |
| `QD-002` | Modelo de dispositivo y cuenta | (a) 1 dispositivo compartido · (b) 2 cuentas, 2 dispositivos · (c) híbrido con modo compartido | Define todo el modelo de privacidad y amenazas | **Difícil** |
| `QD-003` | Local-first vs nube | (a) local-first (sin nube) · (b) nube con cifrado · (c) híbrido | Privacidad, costo, disponibilidad offline, capacidad de análisis | **Difícil** |
| `QD-004` | Flujo de datos al LLM | (a) proveedor con retención cero y sin entrenamiento · (b) modelo local · (c) sin LLM en el MVP | Costo, latencia, calidad, riesgo de fuga | Difícil |
| `QD-005` | Alcance del producto | (a) mantenimiento de relación existente · (b) formación inicial · (c) ambos · (d) individuo que reflexiona solo | Qué modelos se diseñan; "formación" introduce un problema de dominio distinto | Difícil |
| `QD-006` | No-objetivos explícitos | Confirmar: no terapia, no diagnóstico, no compatibilidad, no consejo romántico, no predicción, no red social, no arbitraje | Evita deriva de alcance | Fácil |
| `QD-007` | Piloto con personas reales | (a) sí, con DPIA y consentimiento de investigación · (b) solo datos sintéticos y propios por ahora | Riesgo ético y legal; valor de aprendizaje | Media |
| `QD-008` | Autorización del carril spike | (a) autorizar 1 spike con alcance nombrado · (b) no autorizar | Velocidad de aprendizaje | Fácil |

**Recomendación técnica (no vinculante):** `QD-002` = (c) híbrido con **modo compartido por defecto**; `QD-003` = (a) local-first en el MVP; `QD-004` = (a) con contrato sin entrenamiento y composición por vista; `QD-005` = (a) mantenimiento primero, formación como módulo separado posterior; `QD-007` = (b) primero; `QD-008` = (a).

---

# 18. RIESGOS RESIDUALES: POR QUÉ ESTE SISTEMA TODAVÍA PUEDE FALLAR

Corregir el plan no elimina estos riesgos. Se declaran para que no se descubran tarde.

1. **Fricción real de captura.** La promesa de "baja fricción" compite con el cansancio, el conflicto y la vergüenza de registrar algo vergonzoso. Es el riesgo número uno y solo se resuelve con evidencia de uso.
2. **Techo del autoinforme.** Todo el sistema depende de que las personas reporten con precisión su experiencia. La introspección es limitada y sesgada, y el sistema podría construir hipótesis elegantes sobre datos malos.
3. **Reactividad.** Registrar cambia lo registrado. Si la gente actúa "para el registro", el sistema mide su propia influencia y la confunde con la relación.
4. **El sistema como tercero.** Puede convertirse en una autoridad que las personas usan en conflicto. Mitigado por el lint, pero no eliminado.
5. **Uso asimétrico.** Si una persona usa el sistema mucho más que la otra, aparece una asimetría de información y de poder. No hay control técnico completo contra esto.
6. **Moral licensing.** Documentar la reflexión puede sustituir la conducta ("ya lo registré, ya está").
7. **Ampliación del daño en relaciones coercitivas.** Un sistema que pide reportar eventos íntimos puede aumentar la vigilancia y el riesgo si el agresor accede. `G-SAFE-3` reduce, no elimina.
8. **Falsa autoridad epistémica.** Un sistema con estructura formal (evidencia, hipótesis, experimentos) *parece* más confiable de lo que es con N=2. El formato puede crear la certeza que el contenido niega.
9. **Costo y dependencia de terceros.** Un LLM externo con datos íntimos es un riesgo estructural que una política mitiga pero no borra.
10. **El problema del producto, no de la ingeniería:** puede que nadie quiera un sistema que les devuelva su propia relación como un modelo. Ese es el riesgo que ningún documento resuelve; lo resuelve el spike y, si se autoriza, el piloto.

---

# 19. PRIMERA ACCIÓN DEL AGENTE CON ESTE DOCUMENTO

1. **DETENERSE.** No programar producto.
2. Presentar al humano las decisiones `QD-001` a `QD-008` (§17) con el formato de la Spec §37.
3. Crear únicamente los artefactos de **G0** autorizados por esas decisiones.
4. **No** iniciar G1 hasta que G0 esté aprobada.
5. **No** crear archivos vacíos, ni scaffolding, ni backend, ni base de datos, ni prompts.

---

# FIN DEL PLAN MAESTRO v2

**Estado del proyecto tras esta revisión:**

```text
PROJECT_STATUS        = G0_PENDIENTE_DE_DECISIONES_P0
IMPLEMENTATION_AUTHORIZED = false
SPIKE_AUTHORIZED          = false  (pendiente QD-008)
DOMAIN_MODEL_APPROVED     = false
ARCHITECTURE_APPROVED     = false
MVP_APPROVED              = false
REVIEW_FINDINGS           = 40 hallazgos registrados (§1)
```
