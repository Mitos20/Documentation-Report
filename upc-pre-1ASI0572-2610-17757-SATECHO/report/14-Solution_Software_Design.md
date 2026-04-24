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

---

En el timeline de Asesoría y Configuración de Umbrales, un pain point es la seguridad en la modificación manual. Si el agricultor ingresa un Umbral modificado manualmente con valor fuera de rango seguro, existe el riesgo de que un valor erróneo dañe el cultivo por sobre-riego o bloqueo salino.

En este timeline, un pain point es la sobrescritura de configuraciones. La Aplicación masiva de plantilla por parte del agrónomo podría sobrescribir ajustes previos personalizados por el agricultor sin que este se percate, generando conflictos operativos y desconfianza.

![EventStorming-step3.5](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pain-points-5.png)

---

Después, continuamos con el cuarto paso del DDD llamado Pivotal Points, donde identificamos puntos o eventos comerciales importantes que indicaban un cambio drástico en el contexto, el estado del sistema o la fase del proceso. Estos eventos marcan fronteras naturales entre bounded contexts.

En el flujo de Onboarding e Identidad, el evento Email verificado por el usuario actúa como pivotal point. Marca el cambio irreversible de un visitante anónimo a un usuario autenticado, separando el contexto de adquisición del contexto de gestión de identidad y acceso.

![EventStorming-step4.1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pivotal-points-1.png)

---

En el flujo de Monitoreo y Diagnóstico, el evento Estrés hídrico detectado es pivotal. Indica que el sistema ha pasado de solo recolectar datos brutos (Lectura de humedad) a interpretar el estado fisiológico del cultivo, separando el monitoreo de suelo del diagnóstico agronómico.

En el flujo de Control de Riego, el evento Diagnóstico agronómico generado y posteriormente Riego iniciado son pivotes críticos. El primero separa la capa de análisis de la capa de ejecución; el segundo marca la transición del dominio de software al dominio físico (IoT Device/Actuator), donde una acción en el mundo real es irreversible.

![EventStorming-step4.2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pivotal-points-2.png)

---

En el flujo de Seguridad, el evento Evento clasificado como HUMANO es pivotal. Cambia el contexto de monitoreo pasivo a alerta crítica inmediata, disparando notificaciones externas y requiriendo una política de prioridad alta.

![EventStorming-step4.3](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pivotal-points-3.png)

---

En el flujo de Gestión de Cuentas, los eventos Cuenta de cliente suspendida por mora y Cuenta reactivada tras regularizar pago son pivotes de estado de negocio. Condicionan el acceso a funcionalidades premium y la sincronización de dispositivos IoT.

![EventStorming-step4.4](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pivotal-points-4.png)

---

En el flujo de Dispositivos IoT, el evento Dispositivo iot offline detectado (o falta de heartbeat en 5 min) es pivotal. Cambia el contexto de operación normal a estado de fallo, requiriendo políticas de caché local, encolamiento de comandos y notificación de soporte.

![EventStorming-step4.5](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pivotal-points-5.1.png)

![EventStorming-step4.5](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-pivotal-points-5.2.png)

---

Con todo ello, comenzamos el paso de Commands, donde escribimos el desencadenante de ciertos eventos del dominio, así como el actor encargado.

![EventStorming-step5.1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-1.png)

![EventStorming-step5.2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-2.png)

![EventStorming-step5.3](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-3.png)

![EventStorming-step5.4](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-4.png)

![EventStorming-step5.5](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-5.png)

![EventStorming-step5.6](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-6.png)

![EventStorming-step5.7](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-7.png)

![EventStorming-step5.8](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-8.png)

![EventStorming-step5.9](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-9.png)

![EventStorming-step5.10](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-commands-10.png)

---

Después proseguimos con el paso 6, Policies, donde identificamos eventos que debían ejecutarse en automático o necesitaban alguna política de negocio.

![EventStorming-step6.1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-1.png)

![EventStorming-step6.2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-2.png)

![EventStorming-step6.3](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-3.png)

![EventStorming-step6.4](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-4.png)

![EventStorming-step6.5](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-5.png)

![EventStorming-step6.6](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-6.png)

![EventStorming-step6.7](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-7.png)

![EventStorming-step6.8](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-8.png)

![EventStorming-step6.9](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-policies-9.png)

---

Con ello procedemos a discutir los Read Models, es decir, representaciones visuales que comprenden el flujo del dominio y sirven como proyecciones optimizadas para consultas.

![EventStorming-step7.1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-1.png)

![EventStorming-step7.2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-2.png)

![EventStorming-step7.3](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-3.png)

![EventStorming-step7.4](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-4.png)

![EventStorming-step7.5](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-5.png)

![EventStorming-step7.6](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-6.png)

![EventStorming-step7.7](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-7.png)

![EventStorming-step7.8](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-8.png)

![EventStorming-step7.9](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-9.png)

![EventStorming-step7.10](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-10.png)

![EventStorming-step7.11](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-read-models-11.png)

---

También empezamos a discutir el uso de Sistemas Externos, donde únicamente se encontró necesario en los siguientes servicios.

![EventStorming-step8.1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-external-systems-1.png)

![EventStorming-step8.2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-external-systems-2.png)

![EventStorming-step8.3](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-external-systems-3.png)

![EventStorming-step8.4](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-external-systems-4.png)

---

Después, se comenzó con la identificación de los Aggregates, para ello, tomamos criterios como granularidad, consistencia transaccional y estabilidad del ciclo de vida. Con esos criterios, se procedió a elegir los Aggregates principales.

![EventStorming-step9.1](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-1.png)

![EventStorming-step9.2](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-2.png)

![EventStorming-step9.3](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-3.png)

![EventStorming-step9.4](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-4.png)

![EventStorming-step9.5](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-5.png)

![EventStorming-step9.6](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-6.png)

![EventStorming-step9.7](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-7.png)

![EventStorming-step9.8](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-8.png)

![EventStorming-step9.9](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-9.png)

![EventStorming-step9.10](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-10.png)

![EventStorming-step9.11](upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/candidate-context-discovery/es-aggregates-11.png)