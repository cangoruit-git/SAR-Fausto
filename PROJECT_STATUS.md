# PROJECT_STATUS

**Actualizado:** 2026-09-15
**Puerta actual:** **G0** — Autoridad, alcance y bootstrap
**Implementación autorizada:** ❌ NO

---

## Estado por puerta

| Puerta | Estado | Nota |
| --- | --- | --- |
| **G0** — Autoridad, alcance y bootstrap | 🟡 **EN CURSO** | 2 de 8 decisiones P0 resueltas; falta `docs/SCOPE.md`, `GLOSSARY.md`, `00-GOVERNANCE.md`, `OPEN_QUESTIONS.md` |
| **G1** — Constitución, privacidad y seguridad | ⛔ BLOQUEADA | No abre hasta cerrar G0 |
| **G2** — Semántica del dominio | ⛔ BLOQUEADA | — |
| **G3** — Conocimiento, estrategias y experimentos | ⛔ BLOQUEADA | — |
| **G4** — Requisitos, reglas y no funcionales | ⛔ BLOQUEADA | — |
| **G5** — Diseño técnico | ⛔ BLOQUEADA | — |
| **G6** — MVP e implementación | ⛔ BLOQUEADA | — |

---

## Decisiones P0

| ID | Decisión | Estado | Registro |
| --- | --- | --- | --- |
| `QD-002` | Modelo de dispositivo y cuenta | ✅ **RESUELTA** 2026-09-15 — dos cuentas independientes | [`ADR-0001`](docs/adr/ADR-0001-cuentas-independientes.md) |
| `QD-003` | Local-first vs nube | ✅ **RESUELTA** 2026-09-15 — nube | [`ADR-0002`](docs/adr/ADR-0002-nube.md) |
| `QD-004` | Postura de cifrado: quién puede convertir el cifrado en texto claro | ✅ **RESUELTA** 2026-09-15 — sin custodia de claves por cuenta; el operador puede leer | [`ADR-0003`](docs/adr/ADR-0003-cifrado-sin-custodia-de-claves.md) |
| `QD-001` | Identidad, licencia, visibilidad del repo | ⏳ PENDIENTE | — |
| `QD-005` | Alcance del producto (mantenimiento / formación / individual) | ⏳ PENDIENTE | — |
| `QD-006` | Confirmación de no-objetivos | ⏳ PENDIENTE | — |
| `QD-007` | Piloto con personas reales | ⏳ PENDIENTE | — |
| `QD-008` | Autorización del carril de spikes | ⏳ PENDIENTE | — |

---

## Preguntas abiertas

| ID | Pregunta | Origen | Vence en |
| --- | --- | --- | --- |
| `OQ-001` | ¿Qué ocurre con los artefactos compartidos cuando una cuenta se elimina? | `ADR-0001` §5 | G4 |
| `OQ-002` | ¿La desvinculación se comunica de inmediato o se difiere? | `ADR-0001` §3 | G4 |
| ~~`OQ-003`~~ | Postura de cifrado | `ADR-0002` §8 | ✅ **CERRADA** por `ADR-0003` — el operador puede leer; se compensa con `RET-###`, costura de cifrado y auditoría |

---

## Consecuencias ya en vigor

Lo que las decisiones tomadas **obligan**, y que se incorpora al alcance de G1 y G5. El detalle vive en los ADR; acá solo el puntero.

| Consecuencia | Fuente | Dónde se materializa |
| --- | --- | --- |
| `G-SAFE-3` (dispositivo compartido) **no se elimina**: pasa de default a modo explícito | `ADR-0001` §1 | G1 `SAFETY_MODEL.md` |
| El espacio compartido es **construido, nunca inferido** | `ADR-0001` §2 | G1 `PRIVACY_MODEL.md` |
| La vinculación entre cuentas es una **revelación** y se modela como acto bilateral | `ADR-0001` §3 | G2 `RELATIONSHIP_MODEL.md` |
| **Prohibidos los contadores de actividad cross-account** (por ausencia de superficie) | `ADR-0001` §4 | G4 `BUSINESS_RULES.md` |
| Nuevo adversario **`THR-OPERATOR`** (acceso interno a base y respaldos) | `ADR-0002` §3 | G1 `THREAT_MODEL.md` |
| `INV-PRIV-005` se **amplía** a respaldos y acceso de soporte | `ADR-0002` §3 | G1 `PRIVACY_MODEL.md` |
| **DPIA bloqueante** antes de cualquier dato real | `ADR-0002` §1 | G1 `DPIA-lite.md` |
| Orden de implementación: **columna de privacidad antes que funcionalidades** | `ADR-0001` / `ADR-0002` | G5 `TECHNICAL_ARCHITECTURE_V1.md` |
| Residencia de datos y jurisdicción deben declararse antes del primer dato real | `ADR-0002` §4 | G4 `NON_FUNCTIONAL.md` |
| **Retención máxima con borrado automático y verificable** — la palanca principal de protección | `ADR-0003` §7 | G4 `BUSINESS_RULES.md` (`RET-###`) |
| **Costura de cifrado única**: todo acceso a contenido pasa por un módulo; cada campo declarado `CONTENT` o `METADATA_OPERATIVO` | `ADR-0003` | G5 `DATA_MODEL_V1.md` |
| **Soporte y operaciones sin acceso a contenido** + auditoría de acceso privilegiado | `ADR-0003` | G4 `BUSINESS_RULES.md` + G5 `TECHNICAL_ARCHITECTURE_V1.md` |
| Prohibido el uso de datos reales en desarrollo, staging y demos | `ADR-0003` | G4 `NON_FUNCTIONAL.md` |
| **Cero barrera criptográfica**: `INV-PRIV-001` depende solo de código y de la base | `ADR-0003` §1 | G1 `PRIVACY_MODEL.md` |
| `THR-LEGAL` se materializa: obligación de entrega ante requerimiento judicial | `ADR-0003` §4 | G1 `SAFETY_MODEL.md` (`G-SAFE-5`) |

---

## Riesgo aceptado

| ID | Riesgo | Estado | Revisión obligatoria |
| --- | --- | --- | --- |
| `RISK-001` | El operador, su personal y quien lo obligue legalmente pueden leer contenido íntimo de personas reales. No hay barrera criptográfica. | ⚠️ **ACEPTADO** conscientemente | Antes de `QD-007`; si cambia el alcance; si aparece requisito de cumplimiento; **se detiene** si entran menores |

Compensación en curso: `RET-###` (retención), costura de cifrado, soporte sin contenido, auditoría de acceso. Detalle en [`ADR-0003`](docs/adr/ADR-0003-cifrado-sin-custodia-de-claves.md).

---

## Próxima acción

**`QD-004` ya no bloquea.** G1 sigue bloqueada hasta cerrar **G0**, que ahora requiere:

- decisiones `QD-001`, `QD-005`, `QD-006`, `QD-007`, `QD-008`;
- artefactos `SCOPE.md` (con no-objetivos), `GLOSSARY.md`, `00-GOVERNANCE.md`, `OPEN_QUESTIONS.md`.

**La decisión que ahora condiciona el resto es `QD-007`.** Con `RISK-001` aceptado, dar datos de una pareja real a un sistema que el operador puede leer exige que la retención, el aislamiento y la auditoría ya existan y estén testeados. La recomendación es mantener el piloto con personas reales en ❌ hasta que esos controles pasen sus tests.

---

## Estado del sistema

```text
PROJECT_STATUS            = G0_EN_CURSO
IMPLEMENTATION_AUTHORIZED = false
SPIKE_AUTHORIZED          = false
DOMAIN_MODEL_APPROVED     = false
ARCHITECTURE_APPROVED     = false
MVP_APPROVED              = false
DECISIONES_RESUELTAS      = 3 (QD-002, QD-003, QD-004)
HALLAZGOS_DE_REVISION     = 40 (9 CRITICAL, 19 HIGH, 12 MEDIUM)
RIESGO_ACEPTADO           = RISK-001 (contenido íntimo legible por el operador)
```
