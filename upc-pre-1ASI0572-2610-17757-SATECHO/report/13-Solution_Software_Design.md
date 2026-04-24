# Capítulo IV - Solution Software Design

## 4.1. Strategic-Level Domain-Driven Design

El diseño estratégico de la plataforma AgroSafe se abordó mediante un proceso estructurado de Diseño Orientado al Dominio (DDD). El equipo empleó EventStorming como técnica fundamental para explorar, modelar y comprender el dominio del negocio, seguido de pasos de refinamiento progresivo para identificar contextos delimitados, visualizar flujos de mensajes, definir lienzos de contexto y establecer relaciones de mapeo de contexto.

### 4.1.1. Design-Level EventStorming
El proceso de Event Storming se realizó utilizando la herramienta MIRO, donde construimos todo el flujo de manera colaborativa. Iniciamos con la fase de Exploración No Estructurada, en la que analizamos e intercambiamos ideas sobre los eventos del dominio, siguiendo las buenas prácticas recomendadas. Para la identificación de estos eventos, consideramos criterios como su relevancia, frecuencia y temporalidad.

![EventStorming-step1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/dl-eventstorming/es-events.png)

_Evidencia del desarrollo del primer paso del DDD._

---

Después, avanzamos al segundo paso, denominado **Timelines**, donde analizamos y debatimos la secuencia de los eventos del dominio.

El timeline describe el flujo de un sistema de riego inteligente que inicia con la captura de datos de sensores (humedad, pH y temperatura), analiza condiciones de estrés hídrico y genera un diagnóstico. Con base en ello, ejecuta el riego automáticamente hasta normalizar los valores y finalmente cierra el proceso sincronizando los datos. Después, avanzamos al segundo paso, denominado **Timelines**, donde analizamos y debatimos la secuencia de los eventos del dominio.

El timeline describe el flujo de un sistema de riego inteligente que inicia con la captura de datos de sensores (humedad, pH y temperatura), analiza condiciones de estrés hídrico y genera un diagnóstico. Con base en ello, ejecuta el riego automáticamente hasta normalizar los valores y finalmente cierra el proceso sincronizando los datos.

![EventStorming-step2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/dl-eventstorming/es-timeline.png)

_Evidencia del desarrollo del segundo paso de DDD (Uno de los timelines)._

### 4.1.1.1 Candidate Context Discovery

Para hallar nuestros Candidate Context, continuamos con el paso 3 Pain Points, donde discutimos eventos del flujo que podrían ser cuellos de botella, pasos manuales que requieren automatización o riesgos técnicos críticos que podrían romper la experiencia del usuario o la integridad del cultivo.

En el timeline de Onboarding y Registro, un pain point es la validación de datos duplicados o erróneos en el formulario. Si el sistema no valida en tiempo real el correo o la contraseña, el usuario podría perder toda la información ingresada y abandonar el proceso de registro.

En este timeline, un pain point es la continuidad del wizard de configuración. Si el usuario abandona el flujo a la mitad, el sistema debe poder retomar exactamente donde se dejó; de lo contrario, la fricción aumenta y se pierde la conversión.

![EventStorming-step3.1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pain-points-1.png)

---

En el timeline de Riego y Control de Cultivo, un pain point es la latencia e intermitencia de red en zonas rurales. Específicamente, existe un riesgo crítico entre el Comando de apertura de válvula encolado y la Electroválvula abierta. Si la conexión falla en ese instante, el cultivo podría no recibir el agua necesaria a tiempo.

En este timeline, un pain point es la concurrencia de comandos. Dos usuarios (agricultor y agrónomo) podrían enviar comandos simultáneos para la misma zona generando un conflicto de estado en la electroválvula. Además, si un comando se ejecuta tras recuperar conexión pero supera los 30 minutos, podría regar un cultivo que ya fue hidratado manualmente, generando desperdicio hídrico.

![EventStorming-step3.2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pain-points-2.png)

---

En el timeline de Seguridad Perimetral, un pain point es el riesgo de falsas alarmas. Si el sensor PIR o el algoritmo de clasificación térmica en el Edge no distinguen adecuadamente entre viento, animales pequeños e intrusos humanos, se genera fatiga en el usuario y desconfianza en el sistema.En el timeline de Seguridad Perimetral, un pain point es el riesgo de falsas alarmas. Si el sensor PIR o el algoritmo de clasificación térmica en el Edge no distinguen adecuadamente entre viento, animales pequeños e intrusos humanos, se genera fatiga en el usuario y desconfianza en el sistema.

En este timeline, un pain point es la garantía de entrega de alertas en zonas rurales. Antes de enviar la notificación por WhatsApp, debemos asegurar que el mensaje llegue incluso con cobertura intermitente; de lo contrario, la alerta de intrusión es inútil.

![EventStorming-step3.3](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pain-points-3.png)

---

En el timeline de Gestión de Cuentas y Suscripciones, un pain point es la integridad de los datos históricos. La suspensión de una cuenta por mora NO debe borrar los datos históricos del cultivo; el sistema debe conservar la información para cuando el cliente reactive su servicio.

En este timeline, un pain point es la seguridad de dispositivos perdidos. Un dispositivo IoT reportado como perdido pero con credenciales activas es un riesgo grave, ya que podría enviar telemetría falsa o manipular el riego remotamente.

![EventStorming-step3.4](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pain-points-4.png)
