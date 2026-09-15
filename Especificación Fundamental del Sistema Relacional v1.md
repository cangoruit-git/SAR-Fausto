# ESPECIFICACIÓN FUNDAMENTAL DEL SISTEMA RELACIONAL

**Versión:** 1.0  
**Estado:** Diseño conceptual  
**Tipo:** Documento fundacional del proyecto  
**Propósito:** Definir las reglas, entidades, relaciones y principios que deben respetarse durante el desarrollo del sistema.

---

# 1. PROPÓSITO DEL DOCUMENTO

Este documento define la arquitectura conceptual fundamental de un sistema destinado a ayudar a dos personas a:

- comprender mejor sus propias necesidades, objetivos y patrones;
- comprender mejor la dinámica de su relación;
- detectar patrones recurrentes de interacción;
- distinguir experiencias subjetivas de consecuencias observables;
- identificar posibles sesgos o mecanismos cognitivos sin diagnosticar;
- formular hipótesis;
- consultar conocimiento y evidencia relevante;
- proponer estrategias compatibles con ambas personas;
- realizar pequeños experimentos relacionales;
- observar sus resultados;
- aprender de dichos resultados;
- mantener simultáneamente la autonomía de cada persona y la salud de la relación.

El sistema NO debe reducir una relación a un porcentaje de compatibilidad.

El sistema NO debe intentar determinar quién tiene razón.

El sistema NO debe intentar conservar una relación a cualquier costo.

El sistema NO debe sustituir automáticamente a profesionales de salud mental o terapia de pareja.

El sistema debe funcionar como una infraestructura de observación, reflexión, aprendizaje y experimentación relacional.

---

# 2. PRINCIPIO CENTRAL

La unidad fundamental del sistema no es "la pareja".

La unidad fundamental es:

```text
PERSONA A
+
PERSONA B
+
RELACIÓN
```

Persona A y Persona B son entidades independientes.

La relación es una entidad adicional que surge de la interacción entre ambas.

Conceptualmente:

```text
                 RELACIÓN
                /        \
               /          \
              /            \
       PERSONA A          PERSONA B
```

La relación no debe absorber la identidad de las personas.

Cada persona conserva:

- objetivos propios;
- valores propios;
- necesidades propias;
- límites propios;
- preferencias propias;
- proyectos propios;
- espacio privado;
- autonomía;
- capacidad de aceptar o rechazar estrategias.

La relación contiene:

- objetivos compartidos;
- acuerdos;
- dinámicas;
- patrones;
- conflictos;
- experiencias compartidas;
- estrategias;
- experimentos;
- resultados.

---

# 3. PRINCIPIO DE AUTONOMÍA

El sistema debe asumir que:

> Dos personas pueden elegirse mutuamente sin dejar de ser individuos independientes.

Por lo tanto:

```text
PERSONA A ≠ RELACIÓN
PERSONA B ≠ RELACIÓN

PERSONA A ≠ PERSONA B
```

La relación no constituye una tercera persona.

Es un sistema de interacción.

---

# 4. PRINCIPIO DE NO SACRIFICIO AUTOMÁTICO

Una estrategia no debe considerarse positiva simplemente porque mejore alguna variable de la relación.

Ejemplo:

```text
Beneficio de relación: +10
Costo para Persona A: -20
Beneficio para Persona B: +5
```

No debe clasificarse automáticamente como una buena estrategia.

Toda estrategia debe analizarse al menos desde:

```text
Persona A
Persona B
Relación
Horizonte temporal
```

---

# 5. PRINCIPIO DE MULTIOBJETIVO

El sistema no debe intentar optimizar una única variable.

Debe trabajar con múltiples objetivos simultáneos.

Conceptualmente:

```text
OBJETIVOS PERSONA A
        +
OBJETIVOS PERSONA B
        +
OBJETIVOS RELACIÓN
        +
RESTRICCIONES
        +
LÍMITES
        +
CONSECUENCIAS
```

Una estrategia es una posible configuración.

No es una orden.

El sistema debe buscar configuraciones que permitan compatibilizar objetivos cuando sea posible.

---

# 6. PRINCIPIO DE NO REDUCCIÓN A UNA PUNTUACIÓN

No utilizar como representación principal:

```text
Compatibilidad = 87%
Relación = 72/100
Riesgo = 63%
Calidad = 91%
```

Una relación es multidimensional.

Debe representarse mediante:

- estados;
- tendencias;
- patrones;
- objetivos;
- conflictos;
- experimentos;
- resultados;
- incertidumbre.

Los valores numéricos pueden utilizarse internamente cuando sean necesarios para análisis, pero nunca deben convertirse automáticamente en un "valor de la relación".

---

# 7. PRINCIPIO DE EXPERIENCIA VS CONSECUENCIA

El sistema debe distinguir:

```text
EXPERIENCIA SUBJETIVA
        ↓
INTERPRETACIÓN
        ↓
CONDUCTA
        ↓
CONSECUENCIA
        ↓
RESULTADO A MEDIANO/LARGO PLAZO
```

Que una conducta produzca una sensación positiva inmediata no significa que sea beneficiosa a largo plazo.

Ejemplo:

```text
Conducta:
evitar una conversación

Experiencia inmediata:
alivio

Consecuencia:
problema sin resolver

Consecuencia posterior:
resentimiento

Resultado:
mayor conflicto
```

El sistema debe conservar estas diferencias.

---

# 8. MODELO IMPULSO → CONDUCTA → CONSECUENCIA

Este modelo será una de las estructuras centrales del sistema.

```text
IMPULSO
   ↓
CONDUCTA
   ↓
RESULTADO INMEDIATO
   ↓
CONSECUENCIA
   ↓
RESULTADO POSTERIOR
```

Ejemplo:

```text
Impulso:
retirarme

Conducta:
dejar de responder

Resultado inmediato:
reducción de tensión

Consecuencia:
la otra persona interpreta rechazo

Resultado posterior:
aumento de conflicto
```

El sistema no debe asumir que el impulso determina la conducta.

Debe poder representar:

```text
impulso ≠ conducta
```

Una persona puede sentir un impulso y elegir no actuar según él.

---

# 9. PERSONA

Cada persona debe tener un modelo independiente.

Modelo conceptual:

```text
PERSONA
├── Identidad
├── Valores
├── Objetivos
├── Necesidades
├── Preferencias
├── Límites
├── Hábitos
├── Impulsos
├── Patrones observados
├── Experiencias
├── Interpretaciones
├── Estado actual
└── Información privada
```

---

# 10. IDENTIDAD

La identidad representa información necesaria para distinguir a la persona dentro del sistema.

Debe minimizarse la cantidad de información personal almacenada.

La identidad no debe utilizarse para realizar inferencias innecesarias.

---

# 11. VALORES

Representan principios o aspectos importantes para la persona.

Ejemplos:

```text
Autonomía
Familia
Carrera
Honestidad
Estabilidad
Creatividad
Libertad
Seguridad
Aprendizaje
```

Los valores NO deben convertirse automáticamente en puntuaciones.

---

# 12. OBJETIVO

Un objetivo representa algo que una persona desea alcanzar.

Ejemplos:

```text
Terminar la universidad.
Ahorrar dinero.
Entrenar.
Viajar.
Crear una empresa.
Tener más tiempo personal.
Construir una familia.
```

Cada objetivo puede contener:

```text
Objetivo
├── descripción
├── prioridad personal
├── horizonte temporal
├── estado
├── restricciones
├── progreso
└── posibles interacciones con la relación
```

---

# 13. NECESIDAD

Una necesidad representa algo que una persona considera importante para su bienestar o funcionamiento dentro de un contexto determinado.

Ejemplos:

```text
Tiempo personal
Seguridad
Conexión
Reconocimiento
Autonomía
Descanso
Comunicación
Estabilidad
```

El sistema debe diferenciar:

```text
NECESIDAD
vs
PREFERENCIA
vs
OBJETIVO
vs
LÍMITE
```

No deben ser tratados como sinónimos.

---

# 14. PREFERENCIA

Una preferencia representa una forma deseada de realizar algo, pero que normalmente puede modificarse sin violar necesariamente un límite fundamental.

Ejemplo:

```text
Preferencia:
hablar por la noche.
```

No necesariamente significa:

```text
Necesidad:
hablar por la noche.
```

Esta distinción debe conservarse.

---

# 15. LÍMITE

Un límite representa una condición que una persona establece sobre lo que acepta o no acepta.

Ejemplo:

```text
No quiero discutir mientras estamos gritando.
```

El sistema debe distinguir:

```text
Preferencia
Necesidad
Límite
```

No debe recomendar automáticamente que una persona ignore o viole un límite para beneficiar a la relación.

---

# 16. PERSONA A Y PERSONA B

El sistema debe tratar ambas personas simétricamente a nivel estructural.

```text
PersonA
PersonB
```

Ambas pueden tener:

```text
objetivos
necesidades
preferencias
límites
impulsos
interpretaciones
experiencias
información privada
```

Pero sus contenidos pueden ser completamente diferentes.

No asumir:

```text
A = B
```

ni:

```text
A debe comprender automáticamente lo que B necesita.
```

---

# 17. RELACIÓN

La relación representa el sistema compartido entre ambas personas.

Modelo:

```text
RELACIÓN
├── Personas
├── Objetivos compartidos
├── Acuerdos
├── Expectativas
├── Dinámicas
├── Patrones
├── Conflictos
├── Experimentos
├── Resultados
└── Historia
```

---

# 18. OBJETIVO COMPARTIDO

Un objetivo compartido pertenece al ámbito de la relación.

Ejemplos:

```text
Mejorar la comunicación.
Organizar mejor el tiempo juntos.
Resolver conflictos de manera menos destructiva.
Planificar un viaje.
Construir una rutina conjunta.
```

Un objetivo compartido NO debe reemplazar los objetivos individuales.

---

# 19. CONFLICTO ENTRE OBJETIVOS

El sistema debe permitir representar conflictos como:

```text
Objetivo A
    ↕
Restricción
    ↕
Objetivo B
```

Ejemplo:

```text
A quiere estudiar 4 horas cada noche.

B quiere pasar las noches juntos.

Conflicto:
tiempo disponible.
```

El sistema no debe concluir automáticamente:

```text
A debe ceder.
```

Debe buscar configuraciones alternativas.

Ejemplo:

```text
Configuración 1:
estudio lunes-jueves + tiempo juntos viernes-domingo.

Configuración 2:
estudio temprano + tiempo juntos por la noche.

Configuración 3:
bloques de estudio determinados + bloques de conexión determinados.
```

Las opciones deben presentarse como alternativas a evaluar por las personas.

---

# 20. EVENTO

Un evento representa algo que ocurrió.

Modelo:

```text
EVENTO
├── Fecha/hora
├── Contexto
├── Participantes
├── Descripción
├── Emoción reportada
├── Necesidad percibida
├── Impulso
├── Conducta
├── Interpretación
├── Resultado inmediato
├── Consecuencia posterior
└── Fuente
```

La fuente puede ser:

```text
Persona A
Persona B
Ambos
Sistema
Dato observado
```

---

# 21. OBSERVACIÓN

Una observación debe representar algo reportado o registrado sin convertirlo automáticamente en interpretación.

Ejemplo:

```text
"A dejó de responder durante 3 horas."
```

Esto es diferente de:

```text
"A estaba castigando a B."
```

La primera es una observación.

La segunda es una interpretación.

El sistema debe mantenerlas separadas.

---

# 22. INTERPRETACIÓN

Una interpretación representa el significado que una persona atribuye a un evento.

Ejemplo:

```text
B interpreta:

"Si no responde, significa que no le importo."
```

El sistema debe almacenar:

```text
quién realizó la interpretación
qué interpretación realizó
sobre qué evento
con qué nivel de certeza
```

No debe transformar automáticamente una interpretación en un hecho.

---

# 23. EMOCIÓN

La emoción debe registrarse como experiencia reportada.

Ejemplo:

```text
A:
"Me sentí rechazado."

B:
"Me sentí presionada."
```

El sistema debe respetar:

```text
"sentí X"
```

sin convertirlo automáticamente en:

```text
"X ocurrió objetivamente."
```

---

# 24. IMPULSO

Un impulso representa una tendencia inmediata a actuar.

Ejemplos:

```text
Responder agresivamente.
Retirarse.
Evitar.
Buscar confirmación.
Defenderse.
Controlar.
Cambiar de tema.
Pedir afecto.
```

El sistema debe diferenciar:

```text
impulso
vs
conducta ejecutada
```

---

# 25. CONDUCTA

Representa lo que realmente ocurrió.

Ejemplo:

```text
Impulso:
retirarme.

Conducta:
salí de la habitación.
```

Esto permite estudiar diferencias entre intención e implementación.

---

# 26. CONSECUENCIA

Una consecuencia representa un resultado posterior de una conducta.

Debe distinguir:

```text
resultado inmediato
resultado posterior
resultado recurrente
```

Ejemplo:

```text
Conducta:
evitar conversación.

Resultado inmediato:
menos tensión.

Resultado 24h:
problema sigue presente.

Resultado 7 días:
conflicto recurrente.
```

---

# 27. SESGO O MECANISMO COGNITIVO

El sistema puede identificar posibles mecanismos cognitivos relevantes.

Pero:

```text
POSIBLE MECANISMO ≠ DIAGNÓSTICO
```

Debe expresarse mediante hipótesis.

Ejemplo:

```text
"Los eventos registrados podrían ser compatibles
con una interpretación basada principalmente
en información reciente."
```

Nunca:

```text
"Tienes sesgo X."
```

sin suficiente fundamento.

---

# 28. PATRÓN

Un patrón representa una regularidad observada en múltiples eventos.

No debe declararse un patrón con base en un único evento salvo que exista una razón explícita para ello.

Modelo conceptual:

```text
EVENTO 1
EVENTO 2
EVENTO 3
EVENTO 4
   ↓
REGULARIDAD
   ↓
PATRÓN POTENCIAL
```

Ejemplo:

```text
A se retira durante conflictos.

B busca resolver inmediatamente.

B insiste.

A se retira aún más.

B aumenta la insistencia.

```

Posible patrón:

```text
persecución ↔ retirada
```

El sistema debe formularlo como patrón potencial hasta tener suficiente evidencia.

---

# 29. HIPÓTESIS

Una hipótesis es una explicación provisional.

Ejemplo:

```text
Hipótesis:

Cuando A necesita espacio y no especifica
cuándo retomará la conversación, B interpreta
el silencio como rechazo.

Esto puede provocar que B insista más,
lo cual puede aumentar la retirada de A.
```

Una hipótesis debe contener:

```text
Descripción
Evidencia utilizada
Nivel de confianza
Explicaciones alternativas
Cómo podría comprobarse
```

---

# 30. PRINCIPIO DE INCERTIDUMBRE

El sistema debe poder decir:

```text
No sabemos.
```

Debe evitar falsa certeza.

Estados posibles:

```text
Información insuficiente
Hipótesis débil
Hipótesis plausible
Hipótesis respaldada
Hipótesis contradicha
```

Estos estados no deben interpretarse como diagnósticos.

---

# 31. ESTRATEGIA

Una estrategia representa una posible intervención o modificación de comportamiento.

Ejemplo:

```text
Cuando A necesite espacio:

1. comunicarlo;
2. explicar que necesita una pausa;
3. establecer cuándo retomará la conversación.
```

Cada estrategia debe tener:

```text
Descripción
Objetivo
Persona A
Persona B
Relación
Costos potenciales
Beneficios potenciales
Riesgos
Evidencia
Duración
Condiciones
```

---

# 32. EVALUACIÓN MULTICAPA DE UNA ESTRATEGIA

Toda estrategia debe evaluarse desde:

```text
┌──────────────────────────┐
│ PERSONA A                │
│ beneficios / costos      │
└────────────┬─────────────┘
             │
┌────────────▼─────────────┐
│ PERSONA B                │
│ beneficios / costos      │
└────────────┬─────────────┘
             │
┌────────────▼─────────────┐
│ RELACIÓN                 │
│ beneficios / costos      │
└────────────┬─────────────┘
             │
┌────────────▼─────────────┐
│ TIEMPO                   │
│ corto / medio / largo    │
└──────────────────────────┘
```

No debe existir una sola función de puntuación que determine automáticamente qué estrategia elegir.

---

# 33. EXPERIMENTO RELACIONAL

Una estrategia no debe implementarse necesariamente como regla permanente.

Puede convertirse en experimento.

Modelo:

```text
HIPÓTESIS
   ↓
ESTRATEGIA
   ↓
EXPERIMENTO
   ↓
OBSERVACIÓN
   ↓
RESULTADO
   ↓
APRENDIZAJE
```

---

# 34. PROPIEDADES DEL EXPERIMENTO

Cada experimento debe contener:

```text
Objetivo
Hipótesis
Estrategia
Duración
Condiciones
Participantes
Indicadores
Resultados
Percepción A
Percepción B
Resultado relacional
Efectos secundarios
Conclusión provisional
```

---

# 35. EJEMPLO COMPLETO

## Hipótesis

```text
Cuando A necesita espacio pero no comunica cuándo
retomará la conversación, B puede interpretar el
silencio como rechazo.
```

## Estrategia

```text
A comunica:

"Necesito 30 minutos para tranquilizarme.
Después quiero continuar esta conversación."
```

## Experimento

```text
Duración:
7 días.

Condición:
usar esta estrategia cuando aparezca el patrón.
```

## Medición

Persona A:

```text
Sensación de autonomía
Nivel de estrés
Facilidad para retomar conversación
```

Persona B:

```text
Sensación de seguridad
Sensación de conexión
Ansiedad durante la pausa
```

Relación:

```text
Duración del conflicto
Escalada
Resolución
Recurrencia
```

## Resultado

Puede ocurrir:

```text
A mejora
B mejora
Relación mejora
```

Pero también:

```text
A mejora
B empeora
```

En ese caso el sistema no debe declarar:

```text
estrategia exitosa
```

Debe analizar el conflicto de objetivos.

---

# 36. RESULTADO

Un resultado representa lo ocurrido después de un experimento o conducta.

Debe poder almacenar:

```text
Resultado inmediato
Resultado a 24h
Resultado a varios días
Resultado a largo plazo
Percepción A
Percepción B
Indicadores observables
Efectos secundarios
```

---

# 37. APRENDIZAJE

El sistema debe actualizar hipótesis a partir de resultados.

Ejemplo:

```text
Hipótesis inicial:
la pausa estructurada reducirá el conflicto.

Experimento:
7 días.

Resultado:
reduce escalada pero aumenta sensación
de desconexión en B.

Aprendizaje:
la estrategia podría necesitar un componente
adicional de reconexión.
```

Nueva estrategia:

```text
pausa estructurada
+
mensaje de seguridad
+
retorno acordado
+
reconexión posterior
```

---

# 38. EVIDENCIA

Toda recomendación importante debe conservar su procedencia.

Modelo:

```text
EVIDENCIA
├── Fuente
├── Tipo
├── Contexto
├── Población
├── Resultado
├── Limitaciones
├── Fecha
└── Relación con la estrategia
```

---

# 39. NIVELES DE EVIDENCIA

Utilizar inicialmente:

```text
E1 = Evidencia científica fuerte/relevante
E2 = Investigación observacional
E3 = Casos/documentación profesional
E4 = Testimonios/experiencias
E5 = Hipótesis
```

Estos niveles no deben interpretarse como una escala universal de calidad científica.

Son una clasificación interna para evitar mezclar fuentes de naturaleza diferente.

---

# 40. TESTIMONIOS

Los testimonios pueden utilizarse para:

- generar hipótesis;
- descubrir problemas;
- encontrar estrategias potenciales;
- conocer experiencias humanas;
- identificar casos que la investigación todavía no representa bien.

Pero:

```text
testimonio ≠ evidencia causal
```

No debe utilizarse un testimonio aislado como prueba de que una estrategia funciona.

---

# 41. PRIVACIDAD

El sistema debe separar:

```text
ESPACIO PRIVADO A
ESPACIO PRIVADO B
ESPACIO COMPARTIDO
```

Por defecto:

```text
privado = privado
```

La información privada no debe compartirse automáticamente con la otra persona.

---

# 42. CONSENTIMIENTO

Antes de compartir información privada:

```text
¿Quieres compartir esta información?
```

El consentimiento debe quedar registrado.

El sistema debe evitar convertir la privacidad en una negociación obligatoria.

---

# 43. DATOS DERIVADOS

Debe distinguirse:

```text
dato original
```

de:

```text
inferencia del sistema
```

Ejemplo:

```text
Dato:
"A dijo que necesita más tiempo personal."

Inferencia:
"Existe una posible tensión relacionada con autonomía."
```

La segunda no debe presentarse como hecho.

---

# 44. TRAZABILIDAD

Toda inferencia importante debe poder responder:

```text
¿De dónde salió esta conclusión?
```

Por lo tanto:

```text
Hipótesis
   ↓
Eventos utilizados
   ↓
Datos utilizados
   ↓
Fuente
```

Debe existir trazabilidad.

---

# 45. SEGURIDAD

El sistema debe detectar situaciones en las que no corresponde tratar el problema como una negociación simétrica.

Ejemplos de señales que requieren tratamiento especial:

```text
Violencia
Amenazas
Coerción
Control extremo
Miedo significativo
Abuso
Aislamiento forzado
```

En estas situaciones el sistema no debe recomendar simplemente:

```text
"ambos deben ceder"
```

ni:

```text
"busquen un punto medio"
```

Debe priorizar seguridad y recursos adecuados.

---

# 46. IA

La IA es un componente del sistema.

No es el sistema completo.

Arquitectura conceptual:

```text
DATOS
  ↓
REGLAS DEL SISTEMA
  ↓
CONTEXTO
  ↓
IA
  ↓
PROPUESTA
  ↓
VALIDACIÓN DEL SISTEMA
  ↓
USUARIO
```

No:

```text
Usuario
 ↓
LLM
 ↓
decisión final
```

---

# 47. RESPONSABILIDAD DEL LLM

El LLM puede:

- extraer información;
- resumir;
- detectar posibles patrones;
- formular hipótesis;
- buscar explicaciones alternativas;
- proponer estrategias;
- transformar lenguaje natural en estructuras;
- explicar evidencia;
- generar preguntas.

El LLM no debe tener autoridad absoluta para:

- diagnosticar;
- determinar quién tiene razón;
- decidir qué persona debe sacrificarse;
- revelar información privada;
- declarar una relación buena o mala;
- determinar que una pareja debe continuar o terminar.

---

# 48. MOTOR DE REGLAS

Debe existir una capa determinista alrededor del LLM.

Conceptualmente:

```text
LLM
 ↓
propuesta
 ↓
RULE ENGINE
 ↓
validación
 ↓
resultado permitido
```

El motor de reglas debe verificar:

```text
Privacidad
Consentimiento
Límites
Seguridad
Proveniencia
Estructura
Restricciones
```

---

# 49. PRINCIPIO DE "NO ADIVINAR"

Cuando falte información:

```text
NO INVENTAR.
NO SUPONER.
NO COMPLETAR AUTOMÁTICAMENTE.
```

En su lugar:

```text
pedir información
```

o:

```text
marcar incertidumbre.
```

---

# 50. ARQUITECTURA GENERAL

La arquitectura conceptual completa es:

```text
                       BASE DE EVIDENCIA
                              │
                              ▼
                    ┌──────────────────┐
                    │ MOTOR DE CONOCIMIENTO │
                    └────────┬─────────┘
                             │
                             ▼
┌──────────────┐      ┌──────────────────┐      ┌──────────────┐
│ PERSONA A    │─────►│ MOTOR RELACIONAL │◄─────│ PERSONA B    │
│              │      │                  │      │              │
│ Objetivos    │      │ Patrones         │      │ Objetivos    │
│ Necesidades  │      │ Hipótesis        │      │ Necesidades  │
│ Límites      │      │ Estrategias      │      │ Límites      │
│ Impulsos     │      │ Experimentos     │      │ Impulsos     │
│ Privacidad   │      │ Resultados       │      │ Privacidad   │
└──────────────┘      └────────┬─────────┘      └──────────────┘
                               │
                               ▼
                       ┌───────────────┐
                       │ EXPERIMENTO   │
                       └───────┬───────┘
                               │
                               ▼
                       ┌───────────────┐
                       │ RESULTADOS    │
                       └───────┬───────┘
                               │
                               ▼
                       ┌───────────────┐
                       │ APRENDIZAJE   │
                       └───────┬───────┘
                               │
                               └─────────────► MODELO ACTUALIZADO
```

---

# 51. FLUJO PRINCIPAL DEL SISTEMA

```text
1. Capturar señal
       ↓
2. Registrar evento
       ↓
3. Separar observación e interpretación
       ↓
4. Identificar emoción/necesidad/impulso
       ↓
5. Registrar conducta
       ↓
6. Registrar consecuencias
       ↓
7. Buscar recurrencias
       ↓
8. Generar patrones potenciales
       ↓
9. Formular hipótesis
       ↓
10. Consultar evidencia
       ↓
11. Generar estrategias
       ↓
12. Evaluar A
       ↓
13. Evaluar B
       ↓
14. Evaluar relación
       ↓
15. Evaluar horizonte temporal
       ↓
16. Proponer experimento
       ↓
17. Obtener consentimiento
       ↓
18. Ejecutar
       ↓
19. Medir resultados
       ↓
20. Actualizar hipótesis
       ↓
21. Repetir
```

---

# 52. CAPTURA DE DATOS DE BAJA FRICCIÓN

El sistema debe evitar convertir la relación en trabajo administrativo.

Principio:

> La pareja no debería sentir que tiene que administrar una base de datos para mantener su relación.

Por ello se prioriza:

```text
Check-in rápido
Notas breves
Notas de voz
Registro opcional
Captura después de eventos relevantes
```

No exigir formularios largos diariamente.

---

# 53. SEÑALES EN LUGAR DE REGISTRO TOTAL

No es necesario registrar cada interacción.

El sistema debe buscar:

```text
EVENTOS SIGNIFICATIVOS
+
PATRONES RECURRENTES
+
CAMBIOS
+
CONFLICTOS
+
RESULTADOS
```

---

# 54. MEMORIA TEMPORAL

El sistema debe poder analizar:

```text
Hoy
↓
7 días
↓
30 días
↓
90 días
```

No debe depender únicamente del evento más reciente.

Debe reducir el riesgo de:

```text
recencia
```

y otros errores de interpretación derivados de información demasiado reciente.

---

# 55. DIFERENCIA ENTRE DATOS Y MODELO

El sistema debe conservar:

```text
REALIDAD REPORTADA
```

separada de:

```text
MODELO DEL SISTEMA
```

Ejemplo:

```text
Dato:
B dijo que se sintió ignorada.

Modelo:
podría existir una sensibilidad elevada
ante períodos de silencio.
```

El segundo es una inferencia.

---

# 56. CAMBIOS DE ESTADO

El sistema no debe asumir que las personas son estáticas.

Una persona puede cambiar:

```text
Objetivos
Necesidades
Preferencias
Límites
Contexto
Disponibilidad
Estado emocional
```

Por ello debe existir historial temporal.

---

# 57. VERSIONADO DEL MODELO

Los cambios importantes deben poder rastrearse.

Ejemplo:

```text
Perfil A v1
↓
Perfil A v2
↓
Perfil A v3
```

Esto permite preguntar:

```text
¿Qué cambió?
¿Por qué cambió?
¿Después de qué eventos?
```

---

# 58. NO AUTOMATIZAR EL CONSENTIMIENTO

Una estrategia compartida requiere aceptación.

El sistema puede sugerir:

```text
"Aceptar"
"Modificar"
"Rechazar"
```

No debe asumir consentimiento porque:

```text
la otra persona no respondió
```

---

# 59. EXPERIMENTOS REVERSIBLES

Siempre que sea posible, los experimentos iniciales deben ser:

- pequeños;
- reversibles;
- explícitos;
- medibles;
- de duración limitada.

Ejemplo:

```text
7 días
```

en lugar de:

```text
"cambia esta conducta para siempre."
```

---

# 60. OBJETIVO DEL SISTEMA

El objetivo conceptual NO es:

```text
mantener todas las relaciones.
```

Tampoco:

```text
evitar todas las rupturas.
```

El objetivo es:

> Ayudar a dos personas autónomas a comprender mejor su interacción y explorar formas de relacionarse que puedan ser elegidas voluntariamente por ambas, respetando sus objetivos individuales, límites y bienestar.

---

# 61. PRINCIPIO FUNDAMENTAL

La relación no debe mantenerse a costa de destruir a las personas que la forman.

Pero tampoco debe asumirse que cualquier costo individual significa automáticamente que una estrategia es incorrecta.

Debe analizarse:

```text
Costo
+
Beneficio
+
Voluntariedad
+
Duración
+
Contexto
+
Objetivos
+
Límites
+
Consecuencias
```

---

# 62. ARQUITECTURA DE DATOS INICIAL

Entidades conceptuales mínimas:

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

Estas entidades son conceptuales.

NO implementar todavía la base de datos basándose únicamente en este listado.

Antes de programar se debe realizar una fase de normalización y revisión.

---

# 63. ORDEN DE IMPLEMENTACIÓN

El desarrollo debe seguir este orden:

```text
01. Principios
02. Entidades conceptuales
03. Relaciones entre entidades
04. Reglas de negocio
05. Reglas de privacidad
06. Reglas de seguridad
07. Modelo de datos
08. API
09. Motor determinista
10. Integración LLM
11. Motor de evidencia
12. Experimentos
13. Frontend
14. Observabilidad
15. Métricas
16. Piloto
```

No saltar directamente al frontend.

---

# 64. REGLA PARA EL AGENTE DE DESARROLLO

El agente debe tratar este documento como una especificación fundacional.

Antes de implementar una funcionalidad nueva debe comprobar:

```text
¿Respeta la autonomía individual?
¿Respeta la privacidad?
¿Distingue datos de inferencias?
¿Distingue experiencia de consecuencia?
¿Evita falsa certeza?
¿Respeta límites?
¿Considera A, B y relación?
¿Considera corto, medio y largo plazo?
¿Mantiene trazabilidad?
¿Puede revertirse?
```

Si una funcionalidad contradice estos principios, el agente debe detenerse y reportar el conflicto antes de implementarla.

---

# 65. REGLA CONTRA LA COMPLEJIDAD PREMATURA

No implementar inicialmente:

- cientos de sesgos;
- modelos psicológicos excesivamente complejos;
- predicciones sobre relaciones;
- scoring global;
- automatización completa;
- agentes autónomos con capacidad de modificar datos sensibles sin aprobación;
- recomendaciones irreversibles.

Primero construir:

```text
Modelo pequeño
↓
Datos reales
↓
Pruebas
↓
Validación
↓
Expansión
```

---

# 66. MVP CONCEPTUAL

La primera versión funcional debe contener únicamente:

```text
1. Crear usuario
2. Crear relación
3. Perfil individual básico
4. Objetivos individuales
5. Objetivos compartidos
6. Registro rápido de evento
7. Separación observación/interpretación
8. Registro de emoción
9. Registro de conducta
10. Registro de consecuencia
11. Detección básica de patrones
12. Hipótesis
13. Estrategia
14. Experimento
15. Resultado
16. Historial
17. Privacidad básica
18. Consentimiento
```

No intentar construir el sistema completo desde el principio.

---

# 67. CRITERIO DE ÉXITO DEL MVP

El MVP no debe evaluarse preguntando:

```text
¿la IA dio buenos consejos?
```

Debe evaluarse preguntando:

```text
¿las personas pueden registrar eventos sin fricción?

¿el sistema distingue correctamente observación
de interpretación?

¿las personas entienden las hipótesis?

¿pueden rechazar una hipótesis?

¿pueden modificar una estrategia?

¿pueden realizar un experimento?

¿pueden observar qué ocurrió?

¿se conserva la privacidad?

¿el sistema evita imponer decisiones?
```

---

# 68. PRINCIPIO DE INVESTIGACIÓN

El proyecto debe distinguir:

```text
IDEA
↓
HIPÓTESIS
↓
PROTOTIPO
↓
OBSERVACIÓN
↓
EVIDENCIA
↓
CONCLUSIÓN
```

Nunca:

```text
idea
↓
"funciona"
```

---

# 69. HIPÓTESIS CENTRAL DEL PROYECTO

La hipótesis general del proyecto es:

> Un sistema de apoyo relacional de baja fricción que combine captura mínima de experiencias, detección de patrones, consideración explícita de sesgos e impulsos, conocimiento basado en evidencia y experimentación consensuada podría ayudar a algunas parejas a comprender y modificar dinámicas recurrentes, manteniendo simultáneamente los objetivos individuales de cada persona y los objetivos compartidos de la relación.

Esta afirmación es una:

```text
HIPÓTESIS
```

No un hecho demostrado.

Debe validarse experimentalmente.

---

# 70. DIFERENCIADOR CONCEPTUAL

El sistema NO se define principalmente por:

```text
IA
```

ni por:

```text
chat
```

ni por:

```text
compatibilidad
```

ni por:

```text
consejos románticos
```

Su núcleo diferenciador es:

```text
DOS INDIVIDUOS AUTÓNOMOS
        +
RELACIÓN COMPARTIDA
        +
MEMORIA TEMPORAL
        +
IMPULSO → CONDUCTA → CONSECUENCIA
        +
HIPÓTESIS
        +
EVIDENCIA
        +
EXPERIMENTACIÓN
        +
APRENDIZAJE
```

---

# 71. PRINCIPIO FINAL

La arquitectura debe preservar permanentemente esta idea:

> No optimizar la relación a costa de las personas que la forman.

La finalidad es ampliar las posibilidades de que:

```text
PERSONA A
    │
    │ elige
    ▼
RELACIÓN
    ▲
    │ elige
    │
PERSONA B
```

continúe siendo una relación entre dos personas que **pueden elegirse**, no una estructura que obligue a una persona a desaparecer dentro de ella.

---

# 72. ESTADO DEL DOCUMENTO

Este documento define la especificación conceptual v1.

No debe considerarse definitivo.

Todo cambio importante debe:

1. identificar qué principio modifica;
2. explicar por qué;
3. comprobar qué entidades afecta;
4. comprobar qué reglas afecta;
5. comprobar qué módulos futuros afecta;
6. actualizar la versión del documento.

Versionado recomendado:

```text
v1.0 = especificación conceptual inicial
v1.1 = correcciones menores
v1.2 = ampliaciones compatibles
v2.0 = cambio estructural importante
```

---

# 73. PRÓXIMO DOCUMENTO A CREAR

Una vez aprobado este documento, el siguiente artefacto debe ser:

```text
DATA_MODEL_V1.md
```

Ese documento debe transformar esta especificación conceptual en:

```text
Entidades
Campos
Tipos
Identificadores
Relaciones
Cardinalidades
Restricciones
Índices
Privacidad
Auditoría
Versionado
```

Después:

```text
BUSINESS_RULES_V1.md
```

Después:

```text
API_SPEC_V1.md
```

Después:

```text
AI_ARCHITECTURE_V1.md
```

Después:

```text
EVIDENCE_SYSTEM_V1.md
```

Después:

```text
MVP_IMPLEMENTATION_PLAN.md
```

---

# 74. INSTRUCCIÓN FINAL PARA EL AGENTE

No comenzar todavía a programar el sistema completo.

Primero:

1. Leer este documento completo.
2. Identificar contradicciones internas.
3. Identificar conceptos ambiguos.
4. Identificar entidades faltantes.
5. Identificar reglas que necesiten formalización.
6. Proponer correcciones.
7. NO aplicar cambios estructurales automáticamente.
8. Presentar un informe de revisión.
9. Esperar aprobación.
10. Una vez aprobado, crear `DATA_MODEL_V1.md`.

El agente debe tratar este documento como la fuente conceptual de verdad hasta que exista una versión posterior aprobada.

---

# FIN DE LA ESPECIFICACIÓN FUNDAMENTAL V1