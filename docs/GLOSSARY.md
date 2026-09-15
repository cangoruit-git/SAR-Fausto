# GLOSARIO NORMATIVO

**Versión:** 0.1 (G0)
**Estado:** propuesta — se congela en el cierre de cada puerta
**Rol:** lenguaje ubicuo del proyecto. Todo artefacto posterior **usa estos términos en este sentido**. Si un documento necesita un sentido distinto, se agrega un término nuevo; no se reutiliza el mismo término con otro significado.

Corrige `H-013` (sin glosario) y aporta las definiciones que faltaban para cerrar `H-005`, `H-009` y `H-033`.

---

## 1. Reglas de uso

1. **Un término, un significado.** Sin sinónimos en los artefactos. "Observación" nunca se usa como sinónimo de "evento".
2. **Cada término declara qué NO es.** La mitad del valor del glosario está en las negaciones.
3. **Autoría y visibilidad son obligatorias.** Todo término que represente un enunciado declara quién lo afirma (`§3.1`) y qué visibilidad tiene por defecto (`§3.2`). Sin esos dos datos, un término no puede modelarse.
4. **Los términos prohibidos existen** (`§9`). No son un estilo: son una restricción de producto verificable por test.
5. Los términos en inglés entre paréntesis son el nombre del campo en código; no se usan en la interfaz.

---

## 2. Esquema obligatorio de un término

| Campo | Pregunta que responde |
| --- | --- |
| **Definición** | ¿Qué representa? |
| **NO es** | ¿Con qué se lo confunde y por qué no? |
| **Autoría** | ¿Quién puede afirmarlo? (`A` · `B` · `AMBOS` · `SISTEMA` · `EXTERNO`) |
| **Visibilidad por defecto** | ¿Quién puede leerlo? |
| **Temporalidad** | ¿Tiene intervalo? ¿`occurred_at` distinto de `recorded_at`? |
| **Mutabilidad** | ¿Puede cambiar? ¿Se versiona o se agrega? |

---

## 3. Valores de referencia

### 3.1 Autoría (afirmante)

`A` · `B` · `AMBOS` · `SISTEMA` · `EXTERNO`

Un enunciado **nunca cambia de autoría**. Si el sistema deriva algo y A lo confirma, son **dos** enunciados: uno `INF` (autoría `SISTEMA`) y uno `DEC` (autoría `A`). No se fusionan, no se reescribe la autoría del primero.

### 3.2 Visibilidad

`PRIVATE_A` · `PRIVATE_B` · `SHARED` · `SYSTEM_DERIVED`

- `SYSTEM_DERIVED` **no es visible directamente**. Es la marca de un artefacto producido por el sistema, que solo se muestra a través de una vista (`view(A)`, `view(B)`, `view(shared)`) y cuya visibilidad máxima es la **intersección** de la visibilidad de sus insumos (`INV-PRIV-002`).
- No existe una vista `shared` almacenada (`INV-PRIV-004`). Se renderiza.

### 3.3 Naturaleza epistémica

`REG` (hecho registrado) · `DEC` (declaración de persona) · `INT` (interpretación) · `INF` (inferencia del sistema) · `HYP` (hipótesis) · `EXT` (enunciado externo) · `UNK` (desconocido)

`HYP` **nunca** puede ocupar un campo tipado como evidencia.

---

## 4. Nivel 0 — Lo que ocurrió

| Término (campo) | Definición | NO es | Autoría | Visibilidad por defecto |
| --- | --- | --- | --- | --- |
| **Evento** (`Event`) | Ancla temporal: un intervalo o instante sobre el que alguien registró algo. Es un **índice**, no un relato. | No es "lo que pasó". No tiene descripción única. No tiene verdad. | `SISTEMA` (se crea al registrar) | La del mínimo insumo |
| **Hecho registrado** (`RegisteredFact`) | Lo que el sistema observó directamente: que existió un registro, cuándo, con qué duración, desde qué cuenta. | No es contenido. No es conducta de la persona. | `SISTEMA` | `SYSTEM_DERIVED` |
| **Observación** (`Observation`) | Enunciado **de una persona** sobre hechos perceptibles, sin significado atribuido. "Dejó de responder tres horas." | No es el evento. No es interpretación. **No es verdad objetiva: es un reporte.** | `A` o `B`, obligatoria | `PRIVATE_A` / `PRIVATE_B` según autor |
| **Interpretación** (`Interpretation`) | Significado que **una persona** atribuye a un evento. "Si no responde, no le importo." | No es hecho. No es emoción. No se generaliza al otro. | `A` o `B`, obligatoria | Privada del autor |
| **Emoción** (`Emotion`) | Estado afectivo **reportado** por quien lo vivió. | No es un hecho del mundo. No es una variable de estado del sistema. No es medible por el sistema. | `A` o `B`, obligatoria | Privada del autor |
| **Necesidad percibida** (`PerceivedNeed`) | Lo que una persona reporta necesitar en ese contexto. | No es una necesidad objetiva ni una carencia diagnosticada. | `A` o `B` | Privada del autor |
| **Impulso** (`Impulse`) | Tendencia inmediata a actuar, **reportada**. "Quería irme." | No es la conducta. **Nunca se infiere y se guarda dentro del evento** (`INV-PRIV-009`). | `A` o `B`, obligatoria | Privada del autor |
| **Conducta** (`Behavior`) | Lo que efectivamente ocurrió, según reporte o registro. | No es el impulso. No es la intención. | `A` · `B` · `AMBOS` · `SISTEMA` | La del insumo |
| **Resultado inmediato** (`ImmediateOutcome`) | Efecto percibido en la ventana corta posterior a la conducta. | No es consecuencia a largo plazo. No es "lo que funcionó". | `A` o `B` | Privada del autor |
| **Consecuencia** (`Consequence`) | Efecto posterior, con ventana declarada (24 h, 7 días, más). | No es causa. No es atribuible sin confusores declarados. | `A` · `B` · `AMBOS` | La del insumo |

### 4.1 Reglas duras de este nivel

- **`impulso ≠ conducta`.** El sistema debe poder representar que una persona sintió un impulso y no actuó. Si el modelo los une, el producto miente.
- **`experiencia ≠ consecuencia`.** Que una conducta produzca alivio inmediato no dice nada sobre su efecto posterior. Son campos distintos, con ventanas distintas.
- **`occurred_at ≠ recorded_at`.** Un hecho puede registrarse mucho después de ocurrir. Los dos timestamps existen y no se derivan uno del otro.

---

## 5. Nivel 1 — Lo que se infiere

| Término (campo) | Definición | NO es | Autoría | Visibilidad por defecto |
| --- | --- | --- | --- | --- |
| **Inferencia** (`Inference`) | Enunciado producido por el sistema a partir de otros enunciados. | No es hecho. No es observación. **Nunca se presenta como dato.** | `SISTEMA` | `SYSTEM_DERIVED` (intersección de insumos) |
| **Patrón candidato** (`CandidatePattern`) | Regularidad observada sobre **al menos 3 instancias** en **al menos 2 contextos** distintos. | No es un patrón establecido. No se declara desde un evento único. | `SISTEMA` | `SYSTEM_DERIVED` |
| **Patrón establecido** (`EstablishedPattern`) | Patrón candidato que sobrevivió a la búsqueda activa de **contraejemplos** y sigue vigente tras el período de re-evaluación. | No es una ley. **Decae**: sin instancias nuevas en la ventana definida, vuelve a candidato o se retira. | `SISTEMA` | `SYSTEM_DERIVED` |
| **Contraejemplo** (`Counterexample`) | Instancia registrada que **no** encaja con el patrón. | No es un error de la persona ni del sistema. Es información. | `A` · `B` · `SISTEMA` | La del insumo |
| **Hipótesis** (`Hypothesis`) | Explicación provisional y **falible** sobre por qué ocurre un patrón. | **No es evidencia.** No es diagnóstico. No es conclusión. | `A` · `B` · `SISTEMA` · `CONJUNTA` | La del mínimo insumo entre las que aporta cada persona |
| **Explicación alternativa** (`AlternativeExplanation`) | Otra hipótesis, competidora de la anterior, con el mismo estatus. | No es "la versión débil". Es obligatoria: mínimo 3 hipótesis por lote. | `SISTEMA` | igual que la hipótesis |
| **Señal de seguridad** (`SafetySignal`) | Indicio que **activa una puerta de seguridad**. | **No es conclusión. No es diagnóstico. No es acusación.** Se muestra como señal. | `SISTEMA` (o la persona) | Según `SAFETY_MODEL` (G1) |
| **Confianza** (`Confidence`) | Grado declarado de respaldo de una hipótesis: `débil` · `plausible` · `respaldada` · `contradicha` · `no concluyente`. | No es probabilidad. No es porcentaje. **No es diagnóstico.** | `SISTEMA` | La de la hipótesis |

### 5.1 Reglas duras de este nivel

- **Un patrón nunca se declara desde un evento único.** Sin umbral de instancias y de contextos, no hay patrón: hay anécdota.
- **Toda hipótesis va en lote con alternativas.** El sistema no presenta una sola explicación. La primera explicación generada no puede convertirse en el marco de las siguientes.
- **Toda hipótesis declara cómo se refutaría.** Sin criterio de refutación, no es una hipótesis: es una afirmación disfrazada.
- **`respaldada` no es `hecho`.** Con dos personas, el máximo alcanzable es "los registros son compatibles con esta explicación".

---

## 6. Nivel 2 — Creencia y decisión

| Término (campo) | Definición | NO es |
| --- | --- | --- |
| **Objetivo** (`Goal`) | Algo que una persona quiere alcanzar, con horizonte y prioridad propia. | No es necesidad. No es deseo vago. |
| **Necesidad** (`Need`) | Algo que una persona considera importante para su bienestar en un contexto. | No es preferencia. No es límite. No es carencia diagnosticada. |
| **Preferencia** (`Preference`) | Forma deseada de hacer algo, modificable sin violar un límite. | No es necesidad. No es límite. |
| **Límite** (`Boundary`) | Condición que una persona establece sobre lo que acepta o no acepta. | **No es negociable por el sistema.** No es una preferencia fuerte. |
| **Acuerdo** (`Agreement`) | Compromiso **aceptado explícitamente por ambas partes**, con alcance y vigencia. | No es expectativa. No es suposición. No se presume por silencio. |
| **Expectativa** (`Expectation`) | Lo que una persona espera del otro o de la relación, **declarado o inferido**, sin aceptación de la otra parte. | No es acuerdo. |
| **Conflicto** (`Conflict`) | Incompatibilidad entre objetivos, necesidades o límites de dos partes, o entre una parte y el ámbito compartido. | No es una falta. No tiene culpable. |
| **Estrategia** (`Strategy`) | Configuración de conducta **propuesta**, evaluada por perspectiva y horizonte. | **No es una orden. No es "la mejor". No es recomendación única.** |
| **Experimento** (`Experiment`) | Estrategia convertida en prueba acotada, con pre-registro, línea base, duración, señales de daño y condiciones de cancelación. | No es un cambio permanente. No es un compromiso de conducta futura. |
| **Consentimiento** (`Consent`) | Acto explícito, granular, con alcance y vencimiento, que autoriza un uso concreto de un dato o una participación. | **No se presume. "No respondido" nunca equivale a aceptado.** |

### 6.1 La desambiguación de cuatro vías

Es la confusión más costosa del dominio. Regla operativa:

| Si la persona dice… | Es | Porque |
| --- | --- | --- |
| "Prefiero que me avises antes" | **Preferencia** | Si no se cumple, hay molestia, no daño |
| "Necesito saber que vas a volver" | **Necesidad** | Si no se cumple, se afecta su funcionamiento |
| "Quiero terminar la carrera" | **Objetivo** | Tiene horizonte y estado de progreso |
| "No discuto si estamos gritando" | **Límite** | No es una opción a evaluar; el sistema no la presenta como negociable |

**Regla del sistema:** ante ambigüedad, **preguntar**, no clasificar por defecto. Y si una estrategia solo funciona violando un límite declarado, el sistema **lo dice y no la presenta como opción**.

---

## 7. Nivel 3 — Confianza y gobierno

| Término | Definición | NO es |
| --- | --- | --- |
| **Proveniencia** (`Provenance`) | Lista de identificadores de los insumos que produjeron un artefacto. | No es una explicación narrada. Son IDs verificables. |
| **Artefacto derivado** (`DerivedArtifact`) | Cualquier cosa producida por el sistema a partir de otros datos. | No es "información libre por no ser un dato crudo". Hereda restricciones. |
| **Dato original** (`SourceData`) | Lo que una persona declaró o el sistema registró, sin transformación. | No es interpretación del sistema. |
| **Documento fuente** (`SourceDocument`) | Fuente externa con URL/DOI, fragmento almacenado y appraisal. | No es conocimiento del modelo. |
| **Ausencia de evidencia** (`NO_EVIDENCE_RETRIEVED`) | Resultado válido y frecuente de una búsqueda sin hallazgos aplicables. | **No es un error. No se rellena con lo que el modelo "sabe".** |
| **Escalado de decisión** (`DecisionEscalation`) | Pregunta que el agente debe llevar a una persona antes de continuar. | No es una sugerencia. Bloquea. |

---

## 8. Desambiguaciones críticas

| Confusión frecuente | Por qué importa | Regla |
| --- | --- | --- |
| **Evento vs Observación** | Un evento con un solo relato obliga a adjudicar "quién tiene razón" | El evento es un índice; cada persona aporta su observación. Se admiten **relatos contradictorios** del mismo evento y el sistema **no decide cuál es cierto** |
| **Hecho registrado vs Observación** | Confundir "el sistema vio que se registró" con "esto es lo que pasó" | Un `REG` nunca habla del contenido; una observación nunca es verdad objetiva |
| **Observación vs Interpretación** | Es la separación que el producto entero promete | "Dejó de responder 3 h" = observación. "Me está castigando" = interpretación. Campos distintos, autorías distintas |
| **Impulso vs Conducta** | Si se unen, el sistema atribuye acciones no realizadas | Campos separados; el impulso solo puede ser declarado |
| **Inferencia vs Hipótesis** | Si toda inferencia es hipótesis, nada se puede afirmar; si toda hipótesis es inferencia, todo se vuelve hecho | Inferencia = derivación de datos existentes (contable, verificable). Hipótesis = explicación a contrastar (falible, con alternativas). **Ninguna de las dos es evidencia** |
| **Patrón vs Hipótesis** | Se declara un patrón y se cree que es una explicación | Patrón = *qué* se repite (descriptivo). Hipótesis = *por qué* (explicativo). Primero el patrón, después —y solo si hace falta— la hipótesis |
| **Preferencia vs Necesidad vs Límite** | Determina si algo es negociable | Ver `§6.1` |
| **Acuerdo vs Expectativa** | Lo no acordado se trata como incumplimiento | Solo es acuerdo lo que ambas partes aceptaron explícitamente |
| **Carecer de datos vs Datos que no encajan** | "No sé" se rellena con una suposición | `UNK` es un valor legítimo y frecuente |

---

## 9. Vocabulario prohibido

Términos que **no pueden aparecer** en ninguna salida del sistema (verificable por el lint de `§4.6` del Plan v2 y por `tests/adversarial/`):

| Prohibido | Por qué | En su lugar |
| --- | --- | --- |
| compatibilidad, match, porcentaje de la relación, score | Reduce una relación multidimensional a un escalar | Estados, patrones, conflictos, incertidumbre |
| diagnóstico, "tenés X", "sos X" | Etiqueta clínica sobre una persona | "Los registros son compatibles con…" |
| "el sistema dice que vos…" | Convierte al sistema en árbitro de un conflicto | Atribución explícita y siempre revocable |
| culpable, "quién tiene razón", "el que…" | Adjudica responsabilidad | Descripción de la dinámica, sin culpable |
| "funcionó", "causó", "probado", "significativo" | Afirma causalidad con dos personas | Dirección de cambio dentro de banda, con confusores |
| "tenés que", "deberías" | Prescribe conducta | Alternativas evaluadas, sin orden |
| "siempre", "nunca", "es claro que" | Falsa certeza | Frecuencia observada y su ventana |
| "mejor pareja", "relación sana", "relación tóxica" | Veredicto sobre la relación | Lo que se observa y lo que no se sabe |

---

## 10. Términos pendientes de definición

Se definen en la puerta indicada. **No se usan antes de estar definidos.**

| Término | Puerta |
| --- | --- |
| Ámbito compartido (`SharedSpace`) — cómo existe algo "de la relación" con dos cuentas aisladas | G1 |
| Publicación / revocación (`Publication`, `Revocation`) — acto explícito de poner algo en el ámbito compartido | G1 |
| Retención (`RetentionWindow`) — `RET-###` | G4 |
| Ventana de resultado (`OutcomeWindow`) — cuánto es "inmediato", cuánto "posterior" | G2 |
| Contexto (`Context`) — qué cuenta como "contexto distinto" para el umbral de patrón | G2 |
| Contraejemplo (criterio operativo) | G2 |
| Banda de sin-cambio (`NoChangeBand`) | G2 |
| Rol del profesional externo, si existiera | G4 (hoy: fuera de alcance) |

---

## 11. Estado del documento

Glosario **v0.1**, producido en G0. Cubre los términos que bloqueaban G1 y G2.

**Vigente hasta:** cierre de G0. En ese momento pasa a **v1 y se congela**; a partir de ahí, agregar o redefinir un término requiere un ADR.

Los términos de `§10` están deliberadamente sin definir: definirlos antes de tener el modelo de privacidad (`G1`) sería inventar.
