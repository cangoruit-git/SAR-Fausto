# PLAN MAESTRO DE CONSTRUCCIÓN DEL SISTEMA RELACIONAL

**Documento para el agente de desarrollo — Gentle Pi + Gentle AI + RDD**

**Versión:** 1.0  
**Estado:** Plan maestro de construcción  
**Tipo:** Directiva de proyecto  
**Implementación:** Por fases  
**Regla principal:** NO PROGRAMAR HASTA QUE ESTA DIRECTIVA LO AUTORICE EXPLÍCITAMENTE.

---

# 0. PROPÓSITO DE ESTE DOCUMENTO

Este documento no es solamente una especificación funcional.

Es el **plano de construcción del proyecto**.

El agente debe utilizarlo para determinar:

- qué investigar;
- qué decisiones tomar;
- qué documentos producir;
- qué preguntas hacer;
- qué debe permanecer sin implementar;
- cuándo puede pasar a la siguiente fase;
- cuándo debe detenerse;
- cuándo debe pedir aprobación humana;
- cuándo debe utilizar SDD;
- cuándo debe delegar trabajo;
- cuándo debe verificar;
- y cuándo una fase puede considerarse terminada.

El proyecto debe construirse de forma incremental.

**No se debe intentar construir toda la aplicación desde el principio.**

La arquitectura, el modelo conceptual, las reglas y los límites deben quedar suficientemente definidos antes de escribir código estructural.

---

# 1. REGLA FUNDAMENTAL DEL AGENTE

## 1.1. No convertir este documento inmediatamente en código

El agente NO debe interpretar este documento como una orden para comenzar a crear:

- backend;
- frontend;
- base de datos;
- APIs;
- componentes;
- modelos ORM;
- prompts;
- agentes;
- servicios;
- pipelines;
- infraestructura;
- autenticación;
- dashboards;
- ni cualquier otra implementación.

Primero debe construir el **conocimiento y contrato del sistema**.

El código llegará posteriormente.

---

# 2. OBJETIVO DEL PROYECTO

Construir un sistema capaz de ayudar a dos personas a:

1. conocerse;
2. comprender sus diferencias;
3. identificar patrones de interacción;
4. detectar posibles sesgos e impulsos;
5. diferenciar experiencia subjetiva de consecuencias observables;
6. preservar la autonomía individual;
7. considerar simultáneamente los objetivos de cada persona y los objetivos compartidos;
8. experimentar con estrategias de interacción;
9. observar resultados;
10. aprender de dichos resultados;
11. mantener una relación de manera deliberada;
12. y, eventualmente, ayudar durante la formación inicial de una relación.

El sistema NO debe reducir una relación a:

- compatibilidad;
- puntuaciones;
- porcentajes;
- "match";
- una persona correcta y otra equivocada;
- una única métrica de éxito;
- o una optimización de la pareja a costa de uno de sus integrantes.

---

# 3. PRINCIPIO CENTRAL

La unidad fundamental del sistema NO es "la pareja".

La unidad fundamental es:

> **Dos personas autónomas que deciden relacionarse y una relación que emerge entre ellas.**

Por tanto deben existir tres niveles conceptuales:

```text
PERSONA A
   │
   ├── identidad
   ├── valores
   ├── necesidades
   ├── objetivos
   ├── preferencias
   ├── límites
   ├── impulsos
   ├── experiencias
   └── consecuencias

PERSONA B
   │
   ├── identidad
   ├── valores
   ├── necesidades
   ├── objetivos
   ├── preferencias
   ├── límites
   ├── impulsos
   ├── experiencias
   └── consecuencias

RELACIÓN
   │
   ├── objetivos compartidos
   ├── acuerdos
   ├── dinámicas
   ├── patrones
   ├── conflictos
   ├── experimentos
   └── resultados
```

La relación no debe absorber la identidad de ninguno de los individuos.

---

# 4. PRINCIPIOS INNEGOCIABLES

El agente debe tratar estos principios como restricciones arquitectónicas.

## 4.1. Autonomía

Una persona no existe para optimizar la relación.

La relación tampoco existe para optimizar a una sola persona.

---

## 4.2. No sacrificar automáticamente a una persona

Una estrategia puede beneficiar a la relación y perjudicar a A.

También puede beneficiar a A y perjudicar a B.

También puede beneficiar a ambos y perjudicar la relación a largo plazo.

El sistema debe detectar estos casos.

---

## 4.3. Multiobjetivo

Toda estrategia relevante debe poder evaluarse como mínimo desde:

```text
A
B
RELACIÓN
```

Y cuando sea necesario:

```text
CORTO PLAZO
MEDIANO PLAZO
LARGO PLAZO
```

No debe existir una única función:

```text
relationship_score = ...
```

como representación total del sistema.

---

## 4.4. Experiencia ≠ consecuencia

El sistema debe distinguir:

```text
qué sintió una persona
        ↓
qué interpretó
        ↓
qué hizo
        ↓
qué ocurrió posteriormente
```

Que una conducta produzca una sensación positiva inmediata NO demuestra que sea beneficiosa a largo plazo.

---

## 4.5. Impulso → conducta → consecuencia

Debe poder representarse:

```text
IMPULSO
   ↓
CONDUCTA
   ↓
CONSECUENCIA INMEDIATA
   ↓
CONSECUENCIA POSTERIOR
```

Ejemplo conceptual:

```text
conflicto
   ↓
impulso de retirarse
   ↓
retirada
   ↓
alivio inmediato
   ↓
problema sin resolver
   ↓
distanciamiento posterior
```

El sistema NO debe asumir que este patrón ocurre siempre.

Debe tratarlo como una hipótesis verificable.

---

## 4.6. Los sesgos no son diagnósticos

El sistema puede trabajar con conceptos de psicología cognitiva y comportamiento.

Pero:

```text
posible patrón
```

NO significa:

```text
diagnóstico de la persona
```

Los mecanismos cognitivos deben representarse como:

- hipótesis;
- posibles explicaciones;
- alternativas;
- señales;
- patrones documentados.

Nunca como certeza psicológica automática.

---

## 4.7. No inventar

El agente no debe rellenar vacíos con suposiciones.

Si no existe información suficiente:

```text
UNKNOWN
```

o equivalente explícito.

Debe distinguir:

```text
dato observado
dato declarado
interpretación
hipótesis
inferencia
evidencia externa
```

---

# 5. PRINCIPIO DE BAJA FRICCIÓN

La aplicación no debe convertir el mantenimiento de una relación en trabajo administrativo.

No debe depender de que ambos usuarios:

- rellenen formularios largos diariamente;
- respondan cuestionarios interminables;
- registren manualmente cada interacción;
- clasifiquen cada emoción;
- introduzcan todos los conflictos.

El diseño deberá investigar mecanismos de baja fricción como:

- check-ins mínimos;
- notas de voz;
- entradas opcionales;
- captura contextual;
- eventos importantes;
- memoria temporal;
- análisis posterior.

Pero estas soluciones todavía NO deben implementarse.

Primero deben especificarse.

---

# 6. PRIVACIDAD COMO PARTE DE LA ARQUITECTURA

Debe existir una diferencia entre:

```text
DATOS PRIVADOS DE A
DATOS PRIVADOS DE B
DATOS COMPARTIDOS
DATOS DERIVADOS
```

El sistema NO debe asumir:

```text
dato registrado por A = dato visible para B
```

El consentimiento debe formar parte del modelo.

No debe diseñarse un mecanismo donde una persona pueda utilizar información privada del sistema para manipular a la otra.

---

# 7. SEGURIDAD RELACIONAL

El sistema debe contemplar señales relacionadas con:

- violencia;
- amenazas;
- coerción;
- control;
- aislamiento;
- miedo;
- intimidación;
- abuso;
- manipulación grave.

Pero el sistema NO debe intentar convertirse automáticamente en:

- terapeuta;
- juez;
- diagnosticador;
- investigador forense.

Las señales de seguridad deben conducir a reglas conservadoras y eventualmente a orientación hacia ayuda humana apropiada.

La especificación detallada de esta capa será posterior.

---

# 8. RELACIÓN CON LA EVIDENCIA

El sistema debe separar:

### E1 — Evidencia experimental / investigación controlada

### E2 — Síntesis científica / meta-análisis / revisión sistemática

### E3 — Evidencia observacional

### E4 — Experiencia clínica/documentación profesional

### E5 — Testimonios / experiencias individuales

Estas categorías son una **taxonomía interna de procedencia**, no una afirmación de que toda evidencia científica pueda reducirse perfectamente a cinco niveles.

Los testimonios pueden servir para:

- descubrir patrones;
- generar hipótesis;
- descubrir estrategias posibles.

Pero NO deben transformarse automáticamente en causalidad científica.

---

# 9. EL SISTEMA NO DEBE SER UN SIMPLE CHATBOT

La IA generativa será solamente un componente.

El sistema deberá tener una estructura similar a:

```text
DATOS
  ↓
MODELO
  ↓
REGLAS
  ↓
EVIDENCIA
  ↓
HIPÓTESIS
  ↓
ESTRATEGIAS
  ↓
EXPERIMENTO
  ↓
RESULTADO
  ↓
APRENDIZAJE
```

El LLM podrá ayudar a:

- interpretar lenguaje;
- extraer información;
- resumir;
- generar hipótesis;
- buscar estrategias;
- explicar conceptos;
- adaptar lenguaje.

Pero el LLM NO debe ser la autoridad final del sistema.

---

# 10. ARQUITECTURA CONCEPTUAL OBJETIVO

La arquitectura conceptual inicial es:

```text
             ┌─────────────────────┐
             │     PERSONA A       │
             └──────────┬──────────┘
                        │
                        │
                 ┌──────▼──────┐
                 │  RELACIÓN   │
                 └──────▲──────┘
                        │
                        │
             ┌──────────┴──────────┐
             │                     │
       ┌─────▼─────┐        ┌─────▼─────┐
       │ PERSONA A │        │ PERSONA B │
       └───────────┘        └───────────┘

                    ↓

          OBSERVACIONES / EVENTOS

                    ↓

              PATRONES

                    ↓

             HIPÓTESIS

                    ↓

          EVIDENCIA + CONTEXTO

                    ↓

              ESTRATEGIAS

                    ↓

             EXPERIMENTOS

                    ↓

               RESULTADOS

                    ↓

              APRENDIZAJE
```

Esta arquitectura es conceptual.

NO debe convertirse todavía en clases o tablas.

---

# 11. FASE 0 — INSPECCIÓN DEL ENTORNO

## Objetivo

Antes de modificar cualquier archivo, el agente debe inspeccionar el repositorio.

Debe determinar:

- qué existe;
- qué está implementado;
- qué documentación existe;
- qué stack existe;
- qué tests existen;
- qué infraestructura existe;
- qué convenciones existen;
- qué configuración de Gentle Pi existe;
- qué SDD existe;
- qué skills relevantes están disponibles;
- qué MCP están disponibles;
- qué memoria está disponible;
- qué partes del sistema anterior pueden reutilizarse.

## Regla

NO programar.

## Entregable

Crear únicamente un informe:

```text
docs/project-audit.md
```

El informe debe incluir:

- estado actual;
- tecnologías;
- estructura;
- documentación encontrada;
- riesgos;
- inconsistencias;
- decisiones existentes;
- preguntas abiertas;
- partes inexistentes.

Si existe suficiente contexto previo en Engram, utilizarlo antes de preguntar nuevamente.

---

# 12. FASE 1 — AUDITORÍA DEL CONCEPTO

## Objetivo

Analizar críticamente el concepto del sistema.

El agente debe buscar:

- contradicciones;
- ambigüedades;
- conceptos redundantes;
- conceptos faltantes;
- supuestos no demostrados;
- riesgos éticos;
- riesgos de privacidad;
- riesgos de diseño;
- riesgos de interpretación;
- problemas de medición;
- problemas de causalidad;
- problemas derivados del uso de IA.

Debe intentar encontrar razones por las cuales el sistema podría fallar.

## Regla

NO programar.

## Entregable

```text
docs/concept-audit.md
```

Debe clasificar cada problema como:

```text
CRITICAL
HIGH
MEDIUM
LOW
OPEN QUESTION
```

No resolver silenciosamente decisiones estructurales.

---

# 13. FASE 2 — MODELO HUMANO

Definir formalmente:

```text
Person
Identity
Value
Goal
Need
Preference
Boundary
Impulse
Emotion
Interpretation
Behavior
Consequence
```

Para cada concepto debe definirse:

- significado;
- qué representa;
- qué NO representa;
- origen;
- privacidad;
- temporalidad;
- si puede cambiar;
- si es declarado o inferido;
- grado de confianza;
- relación con otros conceptos.

## Regla

NO crear clases de código.

## Entregable

```text
docs/domain/person-model.md
```

---

# 14. FASE 3 — MODELO DE RELACIÓN

Definir:

```text
Relationship
RelationshipMember
RelationshipGoal
Agreement
SharedValue
SharedNeed
SharedPreference
Conflict
Pattern
```

Debe quedar claro:

- qué pertenece a A;
- qué pertenece a B;
- qué pertenece a ambos;
- qué puede inferirse;
- qué requiere consentimiento;
- qué puede cambiar.

## Regla

NO programar.

## Entregable

```text
docs/domain/relationship-model.md
```

---

# 15. FASE 4 — MODELO DE EVENTOS

Diseñar la representación temporal de acontecimientos.

Conceptualmente:

```text
EVENT
 ├── contexto
 ├── observación
 ├── interpretación
 ├── emoción
 ├── impulso
 ├── conducta
 ├── consecuencia
 ├── fuente
 ├── confianza
 ├── timestamp
 └── privacidad
```

Debe distinguirse:

```text
occurred_at
recorded_at
```

porque un acontecimiento puede registrarse mucho después de haber ocurrido.

## Regla

NO implementar.

## Entregable

```text
docs/domain/event-model.md
```

---

# 16. FASE 5 — SESGOS, IMPULSOS Y MECANISMOS COGNITIVOS

Definir un catálogo inicial de mecanismos potencialmente relevantes.

Por ejemplo:

- confirmation bias;
- attribution bias;
- negativity bias;
- availability/recency effects;
- self-serving bias;
- assumed similarity;
- escalation dynamics;
- emotional reasoning;
- fundamental attribution error.

La lista no es definitiva.

Cada mecanismo debe tener:

```text
nombre
definición
señales posibles
explicaciones alternativas
qué NO permite concluir
riesgos de falso positivo
fuentes
```

## Regla crítica

Nunca:

```text
"detectamos X → persona tiene X"
```

Debe ser:

```text
"los datos son compatibles con X como hipótesis"
```

## Entregable

```text
docs/domain/cognitive-mechanisms.md
```

---

# 17. FASE 6 — MODELO DE CONSECUENCIAS

Debe formalizarse:

```text
ImmediateOutcome
DelayedOutcome
IndividualImpact
RelationshipImpact
Tradeoff
```

Una acción puede tener:

```text
beneficio para A
coste para B
beneficio para relación
coste futuro
```

Por tanto el sistema debe poder representar trade-offs.

## Entregable

```text
docs/domain/outcome-model.md
```

---

# 18. FASE 7 — HIPÓTESIS

El sistema debe separar:

```text
OBSERVACIÓN
      ↓
INTERPRETACIONES POSIBLES
      ↓
HIPÓTESIS
      ↓
EVIDENCIA
      ↓
ESTRATEGIA
```

Una hipótesis nunca debe considerarse automáticamente verdad.

Debe existir la posibilidad de:

```text
Hypothesis A
Hypothesis B
Hypothesis C
```

para evitar que la primera explicación generada por el LLM se convierta en realidad del sistema.

## Entregable

```text
docs/domain/hypothesis-model.md
```

---

# 19. FASE 8 — EVIDENCE ENGINE

Definir cómo el sistema encontrará y utilizará evidencia.

Debe determinarse:

- fuentes permitidas;
- procedencia;
- calidad;
- fecha;
- población estudiada;
- contexto;
- aplicabilidad;
- limitaciones;
- incertidumbre;
- relación entre afirmación y fuente.

No basta con guardar:

```text
source_url
```

Debe existir una relación:

```text
CLAIM
   ↓
EVIDENCE
   ↓
APPLICABILITY
   ↓
LIMITATIONS
```

## Entregables

```text
docs/evidence/evidence-model.md
docs/evidence/evidence-policy.md
```

---

# 20. FASE 9 — STRATEGY ENGINE

Una estrategia debe representar:

```text
Strategy
 ├── objetivo
 ├── contexto
 ├── condiciones
 ├── participantes
 ├── beneficios esperados
 ├── costes potenciales
 ├── riesgos
 ├── evidencia
 ├── alternativas
 └── aplicabilidad
```

No debe existir:

```text
best_strategy
```

como concepto absoluto.

Debe existir:

```text
candidate strategies
```

que se evalúan respecto a:

```text
A
B
RELACIÓN
TIEMPO
RESTRICCIONES
```

---

# 21. FASE 10 — EXPERIMENTOS RELACIONALES

El sistema debe tratar ciertas estrategias como experimentos pequeños y reversibles.

Un experimento debe incluir:

```text
objetivo
participantes
consentimiento
duración
conducta a probar
métricas
señales de éxito
señales de daño
condiciones de cancelación
seguimiento
resultado
```

Nunca debe obligar a una persona a participar.

Cualquiera de los participantes debe poder detener un experimento.

---

# 22. FASE 11 — MEMORIA TEMPORAL

El sistema debe estudiar cómo representar:

```text
evento
→ patrón
→ hipótesis
→ estrategia
→ experimento
→ resultado
```

a lo largo del tiempo.

Debe evitarse que un acontecimiento reciente domine automáticamente toda la interpretación de la relación.

Debe existir consideración de:

- recencia;
- repetición;
- duración;
- cambios;
- contexto;
- eventos excepcionales;
- resultados posteriores.

## Entregable

```text
docs/domain/temporal-memory.md
```

---

# 23. FASE 12 — PRIVACIDAD Y CONSENTIMIENTO

Formalizar:

```text
Consent
PrivacyRule
Visibility
DataOwnership
DerivedData
ConsentScope
```

Debe definirse:

```text
PRIVATE_A
PRIVATE_B
SHARED
SYSTEM_DERIVED
```

y quién puede ver cada elemento.

El agente debe prestar especial atención a los datos derivados.

Una inferencia creada por el sistema a partir de datos privados no debe convertirse automáticamente en información compartida.

## Entregable

```text
docs/privacy/privacy-model.md
```

---

# 24. FASE 13 — SEGURIDAD

Diseñar:

```text
SafetySignal
SafetyContext
SafetyEscalation
```

Debe diferenciarse:

```text
señal
```

de:

```text
conclusión
```

y:

```text
recomendación de seguridad
```

de:

```text
diagnóstico
```

## Entregable

```text
docs/safety/safety-model.md
```

---

# 25. FASE 14 — REQUISITOS DEL SISTEMA

Solo después de terminar las fases conceptuales anteriores se deben convertir los conceptos en requisitos.

Crear:

```text
docs/requirements/SYSTEM_REQUIREMENTS.md
```

Los requisitos deben ser:

- verificables;
- específicos;
- trazables;
- independientes cuando sea posible.

Ejemplo:

```text
REQ-PERSON-001
El sistema debe mantener separados los datos privados de cada participante.
```

---

# 26. FASE 15 — MODELO DE DATOS

Ahora sí se puede comenzar a diseñar el modelo técnico.

Entidades candidatas:

```text
User
PersonProfile
Goal
Need
Preference
Boundary
Value
Relationship
RelationshipMember
RelationshipGoal
Agreement
Event
Observation
Emotion
Interpretation
Impulse
Behavior
Consequence
Pattern
Hypothesis
Evidence
EvidenceSource
Strategy
Experiment
ExperimentParticipant
ExperimentMetric
ExperimentResult
Consent
PrivacyRule
SafetySignal
ModelVersion
AuditEntry
```

Pero esta lista NO es definitiva.

El agente debe justificar:

- cada entidad;
- cada relación;
- cardinalidades;
- ownership;
- lifecycle;
- privacidad;
- versionado;
- trazabilidad.

## Entregable

```text
docs/architecture/DATA_MODEL_V1.md
```

---

# 27. FASE 16 — REGLAS DE NEGOCIO

Crear:

```text
docs/architecture/BUSINESS_RULES_V1.md
```

Debe formalizar reglas como:

```text
BR-AUTONOMY-001
La relación no puede modificar unilateralmente los objetivos individuales.

BR-PRIVACY-001
Los datos privados no se convierten automáticamente en datos compartidos.

BR-HYPOTHESIS-001
Una hipótesis no puede tratarse como hecho sin evidencia adicional.

BR-EXPERIMENT-001
Un experimento relacional requiere consentimiento de los participantes afectados.

BR-EXPERIMENT-002
Cualquier participante puede detener un experimento.

BR-STRATEGY-001
Una estrategia debe considerar impactos individuales y relacionales.
```

La numeración definitiva será determinada posteriormente.

---

# 28. FASE 17 — ARQUITECTURA TÉCNICA

Solo después de completar los modelos anteriores.

Definir:

```text
backend
frontend
database
AI layer
evidence layer
memory
security
observability
testing
deployment
```

El agente debe investigar primero el stack existente.

NO seleccionar tecnologías por preferencia personal.

Debe priorizar:

1. tecnología ya existente en el proyecto;
2. simplicidad;
3. mantenibilidad;
4. coste;
5. seguridad;
6. disponibilidad de documentación;
7. compatibilidad con el proyecto.

## Entregable

```text
docs/architecture/TECHNICAL_ARCHITECTURE_V1.md
```

---

# 29. FASE 18 — AI ARCHITECTURE

La IA debe dividirse conceptualmente en responsabilidades.

Por ejemplo:

```text
Extraction
Classification
Hypothesis generation
Evidence retrieval
Strategy generation
Explanation
Conversation
```

Cada función debe definir:

- input;
- output;
- incertidumbre;
- validación;
- límites;
- fallback;
- si necesita LLM;
- si puede ser determinista.

## Regla

No permitir que el LLM tenga autoridad implícita sobre reglas críticas.

## Entregable

```text
docs/architecture/AI_ARCHITECTURE_V1.md
```

---

# 30. FASE 19 — API CONTRACT

Solo ahora diseñar:

```text
docs/api/API_SPEC_V1.md
```

Antes de implementar endpoints deben estar definidos:

- propósito;
- entrada;
- salida;
- autorización;
- privacidad;
- errores;
- idempotencia cuando corresponda;
- trazabilidad;
- validación.

---

# 31. FASE 20 — MVP

El MVP debe ser deliberadamente pequeño.

Debe demostrar el núcleo del sistema.

Propuesta conceptual:

```text
PERSONAS
   ↓
EVENTOS
   ↓
PATRONES
   ↓
HIPÓTESIS
   ↓
ESTRATEGIAS
   ↓
EXPERIMENTO
   ↓
RESULTADO
```

No intentar construir inicialmente:

- toda la plataforma;
- toda la evidencia científica;
- todos los sesgos;
- todas las funciones sociales;
- un terapeuta virtual;
- una IA omnisciente;
- una red social;
- un sistema de compatibilidad.

---

# 32. FORMACIÓN DE RELACIONES

El proyecto debe contemplar posteriormente un modo distinto:

```text
FORMACIÓN
```

y:

```text
MANTENIMIENTO
```

No deben mezclarse completamente.

En formación deben considerarse:

- intereses;
- valores;
- objetivos;
- límites;
- consentimiento;
- interacción;
- señales;
- incertidumbre;
- conversaciones;
- primeras experiencias.

NO debe producir:

```text
compatibilidad = 87%
```

ni predecir:

```text
esta relación funcionará
```

Debe ayudar a las personas a obtener mejor información para decidir por sí mismas.

---

# 33. PROTOCOLO DE TRABAJO DEL AGENTE

El agente debe seguir este orden general:

```text
INSPECCIONAR
    ↓
COMPRENDER
    ↓
CUESTIONAR
    ↓
DOCUMENTAR
    ↓
REVISAR
    ↓
APROBAR
    ↓
DISEÑAR
    ↓
VERIFICAR
    ↓
IMPLEMENTAR
    ↓
PROBAR
    ↓
REVISAR
    ↓
ENTREGAR
```

Nunca:

```text
PROMPT
  ↓
CÓDIGO
```

para cambios estructurales importantes.

---

# 34. USO DE GENTLE-PI / SDD

Este proyecto es suficientemente amplio para utilizar SDD cuando el agente llegue a cambios de implementación sustanciales.

El agente debe aprovechar las capacidades existentes de Gentle Pi en lugar de crear un SDD paralelo dentro de este documento.

Cuando corresponda, utilizar el flujo de SDD existente:

```text
EXPLORE
→ PROPOSE
→ SPEC
→ DESIGN
→ TASKS
→ APPLY
→ VERIFY
→ ARCHIVE
```

El agente debe respetar los artefactos y contratos de SDD que ya gestione `gentle-pi`.

Este documento define **el contenido y objetivo del proyecto**.

Gentle Pi define **el mecanismo operativo mediante el cual se ejecutan las fases SDD**.

No duplicar el runtime de Gentle Pi.

---

# 35. REGLA DE "NO IMPLEMENTAR"

Durante las fases:

```text
0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
```

el comportamiento predeterminado es:

> **NO PROGRAMAR.**

El agente puede:

- inspeccionar;
- buscar;
- leer;
- investigar;
- comparar;
- documentar;
- modelar;
- proponer;
- detectar problemas.

Pero NO debe implementar funcionalidad.

Si cree que necesita código para validar una hipótesis conceptual, debe detenerse y pedir autorización explícita.

---

# 36. CRITERIO PARA PASAR DE FASE

Una fase no termina porque el agente haya escrito un archivo.

Debe existir:

```text
OBJETIVO CUMPLIDO
+
ARTEFACTO PRODUCIDO
+
CONTRADICCIONES IDENTIFICADAS
+
PREGUNTAS ABIERTAS REGISTRADAS
+
DEPENDENCIAS CONOCIDAS
```

Antes de avanzar debe comprobar:

```text
¿La siguiente fase depende de una decisión todavía no resuelta?
```

Si sí:

```text
STOP
```

y presentar la decisión.

---

# 37. REGLA DE DECISIONES HUMANAS

El agente NO debe decidir silenciosamente sobre:

- principios del sistema;
- privacidad;
- consentimiento;
- arquitectura fundamental;
- definición de conceptos centrales;
- trade-offs importantes;
- cambios de alcance;
- cambios irreversibles;
- riesgos de seguridad;
- decisiones que alteren el propósito del producto.

Debe presentar:

```text
DECISIÓN NECESARIA

Contexto:
...

Opciones:
A:
B:
C:

Consecuencias:
...

Recomendación técnica:
...

Decisión requerida:
...
```

La decisión final corresponde al humano.

---

# 38. USO DE SUBAGENTES

Cuando una tarea requiera explorar muchas partes del proyecto, el agente puede utilizar las capacidades de delegación de Gentle Pi.

Pero debe mantener:

```text
UN OBJETIVO
UN ALCANCE
UN RESPONSABLE
```

para cada trabajo delegado.

No crear una multitud de agentes que modifiquen simultáneamente los mismos archivos.

La coordinación debe permanecer bajo el agente principal.

---

# 39. INVESTIGACIÓN EXTERNA

Cuando una decisión dependa de información externa:

- documentación técnica;
- investigación científica;
- librerías;
- frameworks;
- APIs;
- normativa;
- seguridad;

el agente debe buscar fuentes actuales y registrar la procedencia.

No debe convertir una respuesta de un LLM en fuente primaria.

Cuando una afirmación sea importante para una regla del sistema, debe quedar trazada.

---

# 40. TRAZABILIDAD

Toda parte crítica del sistema debe poder responder:

```text
¿Por qué existe esta regla?
```

La respuesta debe poder remontarse a:

```text
requisito
→ decisión
→ evidencia
→ diseño
→ implementación
→ test
```

Cuando corresponda.

---

# 41. TESTING

Cuando comience la implementación, los tests deben derivarse de:

```text
requirements
+
business rules
+
specifications
+
scenarios
```

No crear tests únicamente para hacer subir cobertura.

Para lógica crítica:

```text
requirement
    ↓
test
    ↓
implementation
    ↓
verification
```

Cuando Gentle Pi/SDD/Strict TDD lo determine, respetar su flujo nativo.

---

# 42. VERIFICACIÓN INDEPENDIENTE

El agente que implementa una funcionalidad no debe ser la única fuente de confianza sobre ella.

Después de implementar:

```text
IMPLEMENT
    ↓
VERIFY
```

La verificación debe comparar:

```text
qué se pidió
vs
qué se construyó
```

y no solamente:

```text
¿compila?
```

---

# 43. RDD

No crear un sistema propio que intente sustituir RDD.

Cuando RDD esté habilitado en el entorno:

- dejar que Gentle AI/gentle-pi gestione su mecanismo;
- no inventar receipts;
- no inventar hashes;
- no afirmar que una revisión RDD ocurrió si no existe evidencia;
- no considerar la narración del agente como prueba;
- respetar los resultados de la revisión nativa;
- no asumir que "terminado" significa "revisado".

RDD trabaja sobre el candidato concreto producido y su evidencia correspondiente.

El agente debe tratar RDD como infraestructura de confianza externa al modelo de dominio.

---

# 44. COMMITS Y DELIVERY

No realizar automáticamente:

```text
commit
push
PR
release
```

salvo que el usuario o la política explícita del repositorio lo solicite.

No confundir:

```text
fase terminada
```

con:

```text
autorización de entrega
```

La política de entrega del repositorio y las reglas de Gentle Pi siguen siendo autoridad separada.

---

# 45. MEMORIA

Si Engram está disponible:

El agente debe aprovecharlo para conservar:

- decisiones;
- descubrimientos;
- contexto;
- problemas;
- decisiones rechazadas;
- decisiones pendientes.

Pero la memoria NO sustituye los documentos fuente del proyecto.

Las decisiones estructurales deben quedar también en archivos versionables cuando corresponda.

---

# 46. REGLA CONTRA LA DERIVA DEL PROYECTO

Si durante la construcción el agente descubre una idea nueva:

```text
NUEVA IDEA
```

no debe introducirla directamente en código.

Debe clasificarla:

```text
BUG
MEJORA
NUEVO REQUISITO
CAMBIO DE ALCANCE
HIPÓTESIS
```

y registrarla.

Si modifica el alcance fundamental:

```text
STOP
```

y solicitar decisión.

---

# 47. REGLA CONTRA LA COMPLEJIDAD PREMATURA

No implementar:

- microservicios innecesarios;
- múltiples bases de datos;
- sistemas distribuidos;
- agentes autónomos complejos;
- pipelines enormes;
- event sourcing;
- sistemas de scoring sofisticados;

solo porque técnicamente son posibles.

Cada componente debe justificar:

```text
problema
beneficio
coste
riesgo
alternativa simple
```

---

# 48. DEFINICIÓN DE "TERMINADO"

Una funcionalidad no está terminada porque:

```text
el código compila
```

Debe cumplir:

```text
requisito
+
reglas
+
tests
+
verificación
+
privacidad
+
seguridad
+
trazabilidad
```

cuando estos sean aplicables.

---

# 49. ORDEN OFICIAL DE CONSTRUCCIÓN

El agente debe respetar este orden salvo decisión humana explícita:

```text
FASE 0
AUDITORÍA DEL PROYECTO

↓

FASE 1
AUDITORÍA DEL CONCEPTO

↓

FASE 2
MODELO HUMANO

↓

FASE 3
MODELO DE RELACIÓN

↓

FASE 4
MODELO DE EVENTOS

↓

FASE 5
SESGOS E IMPULSOS

↓

FASE 6
CONSECUENCIAS Y TRADE-OFFS

↓

FASE 7
HIPÓTESIS

↓

FASE 8
EVIDENCIA

↓

FASE 9
ESTRATEGIAS

↓

FASE 10
EXPERIMENTOS

↓

FASE 11
MEMORIA TEMPORAL

↓

FASE 12
PRIVACIDAD

↓

FASE 13
SEGURIDAD

↓

FASE 14
REQUISITOS

↓

FASE 15
MODELO DE DATOS

↓

FASE 16
REGLAS DE NEGOCIO

↓

FASE 17
ARQUITECTURA TÉCNICA

↓

FASE 18
ARQUITECTURA IA

↓

FASE 19
API

↓

FASE 20
MVP

↓

IMPLEMENTACIÓN

↓

TESTING

↓

VERIFICACIÓN

↓

RDD / REVIEW SI ESTÁ HABILITADO

↓

ENTREGA SEGÚN POLÍTICA DEL REPOSITORIO
```

---

# 50. PRIMERA ACCIÓN DEL AGENTE

Al recibir este documento, el agente NO debe comenzar a programar.

Debe realizar únicamente:

### Paso 1

Inspeccionar el repositorio.

### Paso 2

Inspeccionar la configuración de Gentle Pi disponible.

### Paso 3

Determinar si existe:

- `.pi`;
- SDD;
- Engram;
- skills;
- documentación existente;
- tests;
- código previo.

### Paso 4

Leer los documentos existentes relevantes.

### Paso 5

Crear:

```text
docs/project-audit.md
```

### Paso 6

Crear una lista de:

```text
DECISIONES PENDIENTES
RIESGOS
CONTRADICCIONES
PREGUNTAS
```

### Paso 7

DETENERSE.

No crear backend.

No crear frontend.

No crear base de datos.

No instalar dependencias.

No crear APIs.

No crear modelos ORM.

No crear agentes adicionales.

No crear infraestructura.

No implementar IA.

No asumir decisiones.

---

# 51. PRIMER CHECKPOINT HUMANO

Después de la FASE 0 el agente debe presentar:

```text
AUDITORÍA COMPLETADA

Repositorio:
...

Tecnologías:
...

Estado:
...

Documentación encontrada:
...

Gentle Pi:
...

SDD:
...

Engram:
...

Tests:
...

Riesgos:
...

Preguntas:
...

Decisiones necesarias:
...
```

Y esperar instrucciones.

---

# 52. SEGUNDO CHECKPOINT HUMANO

Después de la auditoría conceptual:

```text
docs/concept-audit.md
```

debe detenerse nuevamente.

No debe pasar automáticamente al diseño técnico.

---

# 53. CHECKPOINTS POSTERIORES

Debe existir una revisión humana antes de pasar de:

```text
concepto
→ modelo

modelo
→ requisitos

requisitos
→ arquitectura

arquitectura
→ implementación
```

Esto evita que un error conceptual inicial se convierta en cientos de archivos de código.

---

# 54. OBJETIVO DEL AGENTE

El objetivo NO es:

> escribir código lo más rápido posible.

El objetivo es:

> construir correctamente el sistema que realmente queremos antes de hacer costoso cambiarlo.

La velocidad de implementación es secundaria frente a:

- claridad;
- trazabilidad;
- seguridad;
- autonomía;
- evidencia;
- mantenibilidad;
- verificabilidad.

---

# 55. REGLA FINAL

Cuando exista incertidumbre importante:

```text
NO INVENTAR
NO PROGRAMAR
NO ASUMIR
NO OCULTAR
```

En su lugar:

```text
IDENTIFICAR
DOCUMENTAR
PROPONER
PREGUNTAR
ESPERAR DECISIÓN
```

---

# 56. ESTADO INICIAL

Al comenzar este proyecto, el estado oficial es:

```text
PROJECT_STATUS = PLANNING

IMPLEMENTATION_AUTHORIZED = false

DOMAIN_MODEL_APPROVED = false

ARCHITECTURE_APPROVED = false

MVP_APPROVED = false
```

Estos estados son conceptuales para este plan.

No deben convertirse automáticamente en variables de código.

---

# 57. RESULTADO ESPERADO

Antes de comenzar la implementación debe existir un conjunto coherente de documentos que permita responder:

```text
¿Qué problema resolvemos?

¿Qué NO intentamos resolver?

¿Qué representa una persona?

¿Qué representa una relación?

¿Cómo representamos acontecimientos?

¿Cómo distinguimos experiencia y consecuencia?

¿Cómo tratamos sesgos?

¿Cómo representamos incertidumbre?

¿Cómo usamos evidencia?

¿Cómo generamos estrategias?

¿Cómo evaluamos trade-offs?

¿Cómo hacemos experimentos?

¿Cómo protegemos la privacidad?

¿Cómo manejamos seguridad?

¿Qué requisitos existen?

¿Cómo se implementará?

¿Cómo se verificará?

¿Qué constituye éxito?
```

Si alguna de estas preguntas críticas permanece sin resolver, el agente debe señalarlo antes de implementar.

---

# 58. PRINCIPIO DE CIERRE

El producto final no debe ser simplemente:

> "una aplicación de parejas con IA".

Debe convertirse en un sistema que ayude a dos personas autónomas a comprender mejor:

```text
a sí mismas
+
a la otra persona
+
la dinámica que crean juntas
```

sin convertir ninguna de las tres cosas en una simplificación excesiva.

La IA debe ayudar a explorar.

La evidencia debe ayudar a fundamentar.

Los experimentos deben ayudar a aprender.

Los datos deben ayudar a recordar.

Las reglas deben proteger.

Pero las decisiones fundamentales sobre la propia vida siguen perteneciendo a las personas.

---

# FIN DEL PLAN MAESTRO