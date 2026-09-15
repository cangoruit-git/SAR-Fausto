# PROJECT_STATUS

**Actualizado:** 2026-09-15
**Puerta actual:** **G0** — Autoridad, alcance y bootstrap
**Implementación autorizada:** ❌ NO

---

## Estado por puerta

| Puerta | Estado | Nota |
| --- | --- | --- |
| **G0** — Autoridad, alcance y bootstrap | 🟡 **EN CURSO** | 5 de 8 decisiones P0 resueltas. Hechos: `README.md`, `LICENSE`, `GLOSSARY.md`, `PROJECT_STATUS.md`, `ADR-0001..0004`. Faltan: `SCOPE.md`, `00-GOVERNANCE.md`, `OPEN_QUESTIONS.md` |
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
| `QD-004` | Postura de cifrado | ✅ **RESUELTA** 2026-09-15 — sin custodia de claves por cuenta; el operador puede leer | [`ADR-0003`](docs/adr/ADR-0003-cifrado-sin-custodia-de-claves.md) |
| `QD-001` | Identidad, licencia, visibilidad | ✅ **RESUELTA** 2026-09-15 — repo público, AGPL-3.0, nombre como homenaje | [`ADR-0004`](docs/adr/ADR-0004-distribucion-autohospedada.md) |
| `QD-005` | Alcance del producto | ✅ **RESUELTA** 2026-09-15 — mantenimiento de una relación existente | Este archivo |
| `QD-009` | Modelo de distribución | ✅ **RESUELTA** 2026-09-15 — código abierto autohospedado como vía primaria | [`ADR-0004`](docs/adr/ADR-0004-distribucion-autohospedada.md) |
| `QD-006` | Confirmación de no-objetivos | ⏳ PENDIENTE | — |
| `QD-007` | Piloto con personas reales | ⏳ PENDIENTE — la decisión que más condiciona | — |
| `QD-008` | Autorización del carril de spikes | ⏳ PENDIENTE | — |

---

## Preguntas abiertas

| ID | Pregunta | Origen | Vence en |
| --- | --- | --- | --- |
| `OQ-001` | ¿Qué ocurre con los artefactos compartidos cuando una cuenta se elimina? | `ADR-0001` §5 | G4 |
| `OQ-002` | ¿La desvinculación se comunica de inmediato o se difiere? | `ADR-0001` §3 | G4 |
| `OQ-004` | ¿Se reabre la postura de cifrado para el perfil autohospedado? Es la única configuración verdaderamente simétrica | `ADR-0004` (`RISK-002`) | G5 |
| `OQ-005` | ¿Qué significa literalmente la sigla «SAR»? | `QD-001` | G0 |
| ~~`OQ-003`~~ | Postura de cifrado | `ADR-0002` §8 | ✅ **CERRADA** por `ADR-0003` |

---

## Consecuencias ya en vigor

Lo que las decisiones tomadas **obligan**. El detalle vive en los ADR; acá solo el puntero.

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
| **Soporte y operaciones sin acceso a contenido** + auditoría de acceso privilegiado | `ADR-0003` | G4 + G5 `TECHNICAL_ARCHITECTURE_V1.md` |
| Prohibido el uso de datos reales en desarrollo, staging y demos | `ADR-0003` | G4 `NON_FUNCTIONAL.md` |
| **Cero barrera criptográfica**: `INV-PRIV-001` depende solo de código y de la base | `ADR-0003` §1 | G1 `PRIVACY_MODEL.md` |
| `THR-LEGAL` se materializa: obligación de entrega ante requerimiento judicial | `ADR-0003` §4 | G1 `SAFETY_MODEL.md` (`G-SAFE-5`) |
| **NFRs de autohospedaje**: un comando de instalación, equipo modesto, respaldo y restauración por no expertos, actualización sin pérdida, `BYO` API key o modelo local | `ADR-0004` | G4 `NON_FUNCTIONAL.md` |
| **Cero telemetría saliente** — el proyecto no sabrá cómo se usa ni cuándo falla | `ADR-0004` §3 | G4 `NON_FUNCTIONAL.md` |
| **La documentación de instalación y verificación es artefacto de producto de primera clase** | `ADR-0004` §5 | G5 / G6 |
| Advertencia obligatoria en la guía de instalación: quien administra la instancia puede leer todo | `ADR-0004` (`RISK-002`) | G6 |

---

## Riesgos aceptados

| ID | Riesgo | Alcance | Estado |
| --- | --- | --- | --- |
| `RISK-001` | El operador, su personal y quien lo obligue legalmente pueden leer contenido íntimo. Sin barrera criptográfica. | **Solo si existe servicio gestionado.** En la vía primaria (autohospedaje) no aplica | ⚠️ Aceptado, alcance reducido por `ADR-0004` |
| `RISK-002` | **Asimetría de administración**: quien instala la instancia puede leer todo. El autohospedaje no es simétrico por defecto | Vía primaria | ⚠️ Aceptado con mitigaciones documentales; mitigación técnica en `OQ-004` (G5) |

**Condiciones de revisión de `RISK-001`:** si se decide ofrecer un servicio gestionado, vuelve con fuerza y exige `RET-###`, aislamiento por fila, auditoría y DPIA antes del primer dato real. Se **detiene** (no se mitiga) si entran menores de edad.

---

## Próxima acción

**`QD-007` es la decisión que más condiciona el resto del proyecto.** El sistema no está implementado y su hipótesis central (`Spec` §69) dice que *podría* ayudar a **algunas** parejas, y no está validada. Antes de invitar a personas reales hace falta que existan y estén testeados la retención, el aislamiento por fila y la auditoría de acceso.

Para cerrar G0 faltan:

- **decisiones:** `QD-006` (no-objetivos), `QD-007` (piloto), `QD-008` (spike);
- **artefactos:** `docs/SCOPE.md` (con no-objetivos), `docs/00-GOVERNANCE.md`, `docs/OPEN_QUESTIONS.md`.

Después de G0, la puerta **G1** produce la columna vertebral: `CONSTITUTION.md`, `PRIVACY_MODEL.md` (`INV-PRIV-001..010`), `SAFETY_MODEL.md` (`G-SAFE-0..6`), `THREAT_MODEL.md` y `DPIA-lite.md`.

---

## Estado del sistema

```text
PROJECT_STATUS            = G0_EN_CURSO
IMPLEMENTATION_AUTHORIZED = false
SPIKE_AUTHORIZED          = false
DOMAIN_MODEL_APPROVED     = false
ARCHITECTURE_APPROVED     = false
MVP_APPROVED              = false
LICENCIA                  = AGPL-3.0
DISTRIBUCION              = autohospedada (via primaria)
VISIBILIDAD_REPO          = publica (pendiente: reescritura de email en historial)
DECISIONES_RESUELTAS      = 6 (QD-001..QD-005, QD-009)
HALLAZGOS_DE_REVISION     = 40 (9 CRITICAL, 19 HIGH, 12 MEDIUM)
RIESGOS_ACEPTADOS         = 2 (RISK-001 con alcance reducido, RISK-002)
```
