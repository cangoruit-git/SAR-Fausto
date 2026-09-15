# SAR-Fausto

Repositorio del **Sistema Relacional** — un sistema en fase de diseño conceptual cuyo objetivo declarado es ayudar a **dos personas autónomas** a comprender sus diferencias, observar patrones de interacción, distinguir experiencia subjetiva de consecuencias observables y experimentar con estrategias de interacción de manera deliberada y consentida.

**Estado actual:** `DISEÑO CONCEPTUAL` — no hay implementación. Ver [PLAN_MAESTRO_v2_CORREGIDO.md](PLAN_MAESTRO_v2_CORREGIDO.md) §19.

> **Definición de "SAR" pendiente** (`QD-001`). El repositorio no tiene todavía nombre de producto, licencia ni visibilidad definidos.

---

## Documentos

| Documento | Rol | Estado |
| --- | --- | --- |
| [PLAN_MAESTRO_v2_CORREGIDO.md](PLAN_MAESTRO_v2_CORREGIDO.md) | **Plano de construcción vigente.** Gobernanza, fases, puertas, taxonomías, invariantes y decisiones pendientes. | Propuesta — requiere aprobación en G0 |
| [Especificación Fundamental del Sistema Relacional v1.md](Especificaci%C3%B3n%20Fundamental%20del%20Sistema%20Relacional%20v1.md) | **Fuente conceptual.** Principios, entidades y reglas del dominio. | Vigente, con correcciones a §39, §62 y §73 |
| [PLAN MAESTRO DE CONSTRUCCIÓN DEL SISTEMA RELACIONAL — AGENTE GENTLE-PI + RDD.md](PLAN%20MAESTRO%20DE%20CONSTRUCCI%C3%93N%20DEL%20SISTEMA%20RELACIONAL%20%E2%80%94%20AGENTE%20GENTLE-PI%20%2B%20RDD.md) | Plan v1. | **Superado en orden, fases y gobernanza** por el Plan v2. Se conserva como histórico |

---

## Principio central

La unidad fundamental del sistema **no es "la pareja"**. Es:

```text
PERSONA A  +  PERSONA B  +  RELACIÓN
```

La relación no debe absorber la identidad de ninguna de las dos personas, y el sistema no debe optimizar la relación a costa de una de ellas.

---

## Reglas duras vigentes

1. **No se programa producto** hasta que la puerta **G6** lo autorice. La única excepción es el carril de *spikes* desechables (§12 del Plan v2), que requiere autorización explícita y opera solo con datos sintéticos o propios.
2. **Sin scoring global.** No existe `relationship_score`, ni compatibilidad, ni veredicto sobre la relación.
3. **Sin diagnóstico.** Los mecanismos cognitivos se expresan como hipótesis, nunca como etiquetas sobre una persona.
4. **Privacidad antes que dominio.** Los invariantes `INV-PRIV-001..010` restringen todos los modelos; se definen en **G1**, antes de la semántica de dominio.
5. **Sin verdad compartida única.** Todo se renderiza por vista: `view(A)`, `view(B)`, `view(shared)`.
6. **Sin evidencia recuperada, no hay evidencia.** El modelo no puede citar literatura desde sus pesos.
7. **No inventar.** La incertidumbre se declara (`UNK`, `NO_EVIDENCE_RETRIEVED`, `NO_CONCLUYENTE`); no se rellena.

---

## Próxima acción

Las decisiones **`QD-001` a `QD-008`** (§17 del Plan v2) están pendientes. Determinan la arquitectura y bloquean la puerta **G0**:

- `QD-001` identidad del producto y licencia
- `QD-002` modelo de dispositivo y cuenta ← *define todo el modelo de privacidad*
- `QD-003` local-first vs nube
- `QD-004` flujo de datos al modelo de lenguaje
- `QD-005` alcance (mantenimiento / formación / individual)
- `QD-006` confirmación de no-objetivos
- `QD-007` piloto con personas reales
- `QD-008` autorización del carril de spikes

---

## Estructura prevista

```text
docs/
  adr/            decisiones (ADR-####)
  privacy/        PRIVACY_MODEL.md, DPIA-lite.md
  safety/         SAFETY_MODEL.md
  security/       THREAT_MODEL.md
  domain/         PERSON_MODEL.md, RELATIONSHIP_MODEL.md, EVENT_MODEL.md, …
  evidence/       EVIDENCE_MODEL.md, EVIDENCE_POLICY.md, SEARCH_PROTOCOL.md
  requirements/   SYSTEM_REQUIREMENTS.md, NON_FUNCTIONAL.md, BUSINESS_RULES.md
  architecture/   DATA_MODEL_V1.md, TECHNICAL_ARCHITECTURE_V1.md, AI_ARCHITECTURE_V1.md
  api/            API_SPEC_V1.md
  spikes/         SPIKE-###.md
openspec/         (solo cuando SDD se active en G5/G6)
```

**Regla:** no se crean archivos vacíos. Cada archivo nace con contenido en la puerta que lo produce.

---

## Idioma

Los artefactos del proyecto se escriben en **español** (convención existente del repositorio). El código, los identificadores y los mensajes de commit usan **inglés** cuando sean artefactos técnicos.
