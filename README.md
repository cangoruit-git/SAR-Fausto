# SAR-Fausto

Sistema relacional: software libre para que **dos personas autónomas** comprendan sus diferencias, observen sus patrones de interacción, distingan experiencia subjetiva de consecuencias observables y prueben estrategias de interacción de forma deliberada y consentida.

**Estado:** `G0` — diseño conceptual. **No hay implementación.** Ver [PROJECT_STATUS.md](PROJECT_STATUS.md).

> **Sobre el nombre.** «Fausto» es un homenaje doméstico y no refiere a ninguna persona. No hay ninguna persona real asociada a este repositorio.
>
> La sigla «SAR» todavía no tiene significado oficial (`OQ-005`).

---

## Cómo se distribuye

**Autohospedado, y eso no es un detalle técnico: es la decisión que hace que el sistema sea honesto.**

Cada pareja corre su propia instancia. El operador del sistema es la propia pareja, así que nadie más puede leer lo que hay adentro. Si el proyecto ofreciera un servicio gestionado, quien lo opera podría leer la intimidad de gente que no conoce — y tendría que entregarla si un juez lo requiere. Autohospedado, ese problema no existe.

**Consecuencia que hay que decir en voz alta:** el autohospedaje limita el alcance a las parejas con comodidad técnica. Llegar a "muchas parejas" exige resolver el empaquetado y la instalación, y eso es trabajo de producto pendiente, no una consecuencia automática de tener el código abierto. Ver [`ADR-0004`](docs/adr/ADR-0004-distribucion-autohospedada.md).

**Advertencia de administración:** quien instala y administra una instancia puede leer todos los datos que contiene. Si una sola persona de la pareja la instala, obtiene ese poder y la otra no necesariamente lo sabe. El autohospedaje no es simétrico por defecto (`RISK-002`).

---

## Licencia

**GNU Affero General Public License v3.0** — ver [LICENSE](LICENSE).

Se eligió AGPL y no MIT por una razón concreta: este sistema maneja datos íntimos, y su garantía de privacidad depende enteramente de que el código se comporte como dice. AGPL obliga a publicar el código completo a cualquiera que ofrezca el sistema como servicio en red. **Eso significa que nadie puede quedarse con la intimidad de las parejas adentro de una caja negra.**

---

## Documentos

| Documento | Rol | Estado |
| --- | --- | --- |
| [PROJECT_STATUS.md](PROJECT_STATUS.md) | **Estado vivo del proyecto.** Puertas, decisiones, riesgos. | Vigente |
| [PLAN_MAESTRO_v2_CORREGIDO.md](PLAN_MAESTRO_v2_CORREGIDO.md) | **Plano de construcción.** Gobernanza, puertas, taxonomías, invariantes. | Propuesta — requiere aprobación en G0 |
| [docs/GLOSSARY.md](docs/GLOSSARY.md) | **Lenguaje normativo.** Qué significa cada término y qué no. | v0.1 |
| [docs/adr/](docs/adr/) | Decisiones de arquitectura, con sus consecuencias y lo que obligan. | 4 ADR aceptados |
| [Especificación Fundamental del Sistema Relacional v1.md](Especificaci%C3%B3n%20Fundamental%20del%20Sistema%20Relacional%20v1.md) | **Fuente conceptual.** Principios, entidades y reglas del dominio. | Vigente, con correcciones a §39, §62 y §73 |
| [PLAN MAESTRO DE CONSTRUCCIÓN DEL SISTEMA RELACIONAL — AGENTE GENTLE-PI + RDD.md](PLAN%20MAESTRO%20DE%20CONSTRUCCI%C3%93N%20DEL%20SISTEMA%20RELACIONAL%20%E2%80%94%20AGENTE%20GENTLE-PI%20%2B%20RDD.md) | Plan v1. | **Superado** en orden, fases y gobernanza. Se conserva como histórico |

---

## Principio central

La unidad fundamental del sistema **no es "la pareja"**. Es:

```text
PERSONA A  +  PERSONA B  +  RELACIÓN
```

La relación no debe absorber la identidad de ninguna de las dos personas, y el sistema no debe optimizar la relación a costa de una de ellas.

---

## Reglas duras vigentes

1. **No se programa producto** hasta que la puerta **G6** lo autorice.
2. **Sin scoring global.** No existe `relationship_score`, ni compatibilidad, ni veredicto sobre la relación.
3. **Sin diagnóstico.** Los mecanismos cognitivos se expresan como hipótesis, nunca como etiquetas sobre una persona.
4. **Privacidad antes que dominio.** Los invariantes `INV-PRIV-001..010` restringen todos los modelos; se definen en **G1**.
5. **Sin verdad compartida única.** Todo se renderiza por vista: `view(A)`, `view(B)`, `view(shared)`. Se admiten **relatos contradictorios** del mismo evento y el sistema no decide cuál es cierto.
6. **Sin evidencia recuperada, no hay evidencia.** El modelo no puede citar literatura desde sus pesos.
7. **No inventar.** La incertidumbre se declara (`UNK`, `NO_EVIDENCE_RETRIEVED`, `NO_CONCLUYENTE`); no se rellena.
8. **Vocabulario prohibido.** Hay términos que el sistema no puede emitir, y son verificables por test. Ver [docs/GLOSSARY.md](docs/GLOSSARY.md) §9.

---

## Alcance del MVP

**Mantenimiento de una relación existente** (`QD-005`): dos personas que ya están juntas y quieren entenderse mejor. Modelos: relación, acuerdos, patrones, experimentos.

**Fuera del MVP:** formación inicial de vínculos, compatibilidad, predicción, formación/recomendación de terapia.

---

## Próxima acción

Faltan tres decisiones (`QD-006`, `QD-007`, `QD-008`) y tres artefactos de G0 (`SCOPE.md` con no-objetivos, `00-GOVERNANCE.md`, `OPEN_QUESTIONS.md`). El detalle está en [PROJECT_STATUS.md](PROJECT_STATUS.md).

---

## Idioma

Los artefactos del proyecto se escriben en **español** (convención del repositorio). El código, los identificadores y los mensajes de commit usan **inglés**.
