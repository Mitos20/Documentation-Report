# Capítulo IV - Solution Software Design

## 4.1. Strategic-Level Domain-Driven Design

El diseño estratégico de la plataforma AgroSafe se abordó mediante un proceso estructurado de Diseño Orientado al Dominio (DDD). El equipo empleó EventStorming como técnica fundamental para explorar, modelar y comprender el dominio del negocio, seguido de pasos de refinamiento progresivo para identificar contextos delimitados, visualizar flujos de mensajes, definir lienzos de contexto y establecer relaciones de mapeo de contexto.

### 4.1.1. Design-Level EventStorming
El proceso de Event Storming se realizó utilizando la herramienta MIRO, donde construimos todo el flujo de manera colaborativa. Iniciamos con la fase de Exploración No Estructurada, en la que analizamos e intercambiamos ideas sobre los eventos del dominio, siguiendo las buenas prácticas recomendadas. Para la identificación de estos eventos, consideramos criterios como su relevancia, frecuencia y temporalidad.El proceso de Event Storming se realizó utilizando la herramienta MIRO, donde construimos todo el flujo de manera colaborativa. Iniciamos con la fase de Exploración No Estructurada, en la que analizamos e intercambiamos ideas sobre los eventos del dominio, siguiendo las buenas prácticas recomendadas. Para la identificación de estos eventos, consideramos criterios como su relevancia, frecuencia y temporalidad.

![EventStorming-step1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/dl-eventstorming/es-events.png)

_Evidencia del desarrollo del primer paso del DDD._

---

Después, avanzamos al segundo paso, denominado **Timelines**, donde analizamos y debatimos la secuencia de los eventos del dominio.

El timeline describe el flujo de un sistema de riego inteligente que inicia con la captura de datos de sensores (humedad, pH y temperatura), analiza condiciones de estrés hídrico y genera un diagnóstico. Con base en ello, ejecuta el riego automáticamente hasta normalizar los valores y finalmente cierra el proceso sincronizando los datos. Después, avanzamos al segundo paso, denominado **Timelines**, donde analizamos y debatimos la secuencia de los eventos del dominio.

El timeline describe el flujo de un sistema de riego inteligente que inicia con la captura de datos de sensores (humedad, pH y temperatura), analiza condiciones de estrés hídrico y genera un diagnóstico. Con base en ello, ejecuta el riego automáticamente hasta normalizar los valores y finalmente cierra el proceso sincronizando los datos.

![EventStorming-step2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/dl-eventstorming/es-timeline.png)

_Evidencia del desarrollo del segundo paso de DDD (Uno de los timelines)._