# Capítulo I - Introducción

## 1.1. Startup Profile

En esta sección, se presenta el overview general sobre cómo surge la startup SATECHO considerando los principales indicios que contribuyeron en su fundación. Adicional a ello, comprenderán la misión y visión que SATECHO espera lograr y ofrecer como valor a sus clientes y, conocerán más de cerca el perfil profesional del equipo que forma parte de esta expedición tecnológica.

### 1.1.1. Descripción de la Startup

SATECHO es una startup tecnológica fundada el 4 de abril de 2026 por un equipo de ingenieros universitarios decididos a resolver una problemática crítica: **la vulnerabilidad del agricultor frente a climas impredecibles y la inseguridad en sus tierras**. Observamos que la falta de datos exactos y la dependencia de procesos manuales generan pérdidas masivas de cultivos y recursos hídricos. Ante esto, nacemos para transformar el esfuerzo físico en una gestión estratégica mediante el uso de tecnologías IoT.

Nos especializamos en el desarrollo de sistemas de monitoreo en tiempo real que mitigan los riesgos de la variabilidad climática y las brechas de seguridad. Para ello, implementamos nodos sensores que miden con precisión la humedad del suelo y el ambiente, utilizando microcontroladores ESP32, conocidos en la industria por su robusta capacidad de procesamiento y conectividad inalámbrica integrada. Esto nos permite garantizar que cada gota de agua se utilice solo cuando el cultivo realmente lo necesita, activando sistemas de riego de forma automática y precisa.

En SATECHO, democratizamos la agricultura con precisión: hacemos que la tecnología sea tan fácil de usar como revisar un mensaje de texto, permitiendo que cualquier persona proteja su inversión y optimice su producción desde la palma de su mano.

**Misión:**

Nuestra misión es poner la tecnología al servicio de las personas que trabajan la tierra y de los profesionales que la gestionan. En SATECHO, creamos sistemas de monitoreo amigables que ayudan al agricultor a cuidar sus insumos y brindar al ingeniero agrónomo datos precisos para proteger los cultivos de manera automática. Buscamos que el equipo del campo pueda tomar mejores decisiones basadas en evidencias, evitando pérdidas y trabajando con la tranquilidad de un cultivo siempre vigilado e hidratado.

**Visión:**

Aspirar para el año 2030, ser el aliado tecnológico principal de los pequeños y medianos agricultores en las regiones rurales del Perú y la zona andina, liderando la transición hacia una agricultura de precisión inclusiva, donde agricultores e ingenieros colaboren mediante soluciones de hardware y software que respetan la realidad del campo, manteniendo la excelencia en la arquitectura de nuestros sistemas embebidos y la calidez en nuestro servicio.

### 1.1.2. Perfiles de integrantes del equipo

| Foto de Perfil | Nombre Completo | Descripción |
| :---: | :---: | :--- |
| ![Jose Diego`s Photo](/upc-pre-1ASI0572-2610-17757-SATECHO/report/assets/images/Jose-Diego.jpg) | José Diego Huamani Sánchez (U202110458) | Soy estudiante de la carrera de Ingeniería de software con 22 años de edad el cual tiene una enorme pasión por la ingeniería de datos, dirección de equipos y la toma de decisiones estratégicas que se pueden profundizar mediante el uso de la tecnología. Primordialmente estaré asumiendo el rol de **Team Leader** para planificar y monitorear cada uno de los avances estipulados durante cada sprint así como medir la madurez y el progreso alcanzado a nivel individual como organizacional para permitir elaborar estrategias competitivas y feedbacks. Dentro de mis conocimientos radican la gestión de proyectos agiles con el framework SCRUM, la analítica de datos y big data usando herramientas como Pandas, Numpy y PySpark, desarrollo de aplicaciones web mediante frameworks como Angular y Astro, servicios backend con tecnologías como .NET y Fast API, y entornos Cloud como el Microsoft Azure. |

## 1.2. Solution Profile

Conoceremos los detalles acerca de los antecedentes y problemáticas que son las principales claves para asentar las bases de la investigación sobre la propuesta de solución hacia el sector agrícola.

### 1.2.1. Antecedentes y problemáticas

**Técnica de las 5W's y 2H's**

* Who (Quién):

    **- Usuarios principales:**
    
    - **Agricultor:** Aporta la experiencia empírica y la intuición. Su problema es la dependencia de la presencia física humana y la falta de datos exactos para validar sus decisiones.
    
    - **El Ingeniero Agrónomo:** Busca optimizar el rendimiento y evitar la pérdida del cultivo mediante evidencia científica. Su problema es la dificultad de recolectar datos en tiempo real de múltiples puntos del terreno simultáneamente.

    **- Clientes Objetivo:** Pequeñas y medianas empresas (PYMES) del sector agrícola en Latinoamérica que buscan transitar de operaciones manuales a una gestión basada en datos para reducir pérdidas.

    **- Equipo del Proyecto (SATECHO Core Team):**
    
    - **Project Leader:** Responsable de la visión estratégica y el cumplimiento de hitos.
    
    - **Ingenieros de IoT:** Encargados del diseño de hardware, selección de sensores y arquitectura de nodos.
    
    - **Ingenieros de Software:** Desarrolladores de la infraestructura web/móvil y la lógica de comunicación HTTP.

    - **Especialista en UX/Agro:** Encargado de que la interfaz sea comprensible para el agricultor, simplificando datos complejos.

* What (Qué):

    **El Desafío:** La falta de un sistema integrado que unifique la seguridad perimetral con el control y supervisión automatizada de cultivos. Actualmente, estos problemas se tratan por separado, aumentando los costos.

    - **Modelo de Servicio:** Implementaremos un modelo **Freemium**.
        - **Básico:** Monitoreo de datos históricos.
        - **Premium:** Alertas en tiempo real, automatización avanzada de válvulas y reportes analíticos de salud del cultivo.
    
* Where (Dónde):

    - **Entorno Físico:** Parcelas y terrenos agrícolas de escala media donde la conectividad suele ser un reto y la supervisión humana es insuficiente por la extensión del área.

    - **Mercado Objetivo:** Iniciando en regiones agrícolas emergentes de Perú, con proyección de escalabilidad a toda la región andina y América Latina.
    
* When (Cuando)
    - **Ciclo de Uso:** El cliente interactúa con el producto diariamente. El evento crítico ocurre cuando las variables ambientales (humedad/humo) se desvían de los rangos de seguridad proyectados por el ingeniero agrónomo y/o especialistas del área.

    - **Tiempo de Respuesta:** La problemática actual es que el agricultor se entera del daño "horas o días después". SATECHO busca reducir ese tiempo a "segundos" tras la detección.
    
* Why (Por qué):
    - **Causa Raíz:** El cambio climático ha vuelto obsoleta la intuición pura del agricultor. Las sequías repentinas, lluvias intensas u otro factor climatológico se pueden pronosticar pero no avisan.

    - **Desencadenante:** El aumento en los costos de insumos (agua y fertilizantes) por el aumento de plagas y el incremento de la inseguridad en zonas rurales obligan a las empresas a buscar eficiencia operativa para sobrevivir económicamente.
    
* How (Cómo):
    - **Condiciones Actuales:** Las decisiones se toman bajo incertidumbre. El riego se hace "por calendario" y no "por necesidad", lo que genera desperdicio.

    - **Preferencias del Usuario:** El usuario prefiere no tener que configurar códigos complejos; busca una solución "Plug & Play" que se adapte a su rutina diaria sin interrumpirla.
    
* How Much (Cuánto):
    - **Cuantificación del Daño:** Pérdidas estimadas de entre el **15% y 30%** de la producción total por mala gestión de riego o intrusiones no detectadas.

    - **Inversión y Lanzamiento:** El objetivo es lanzar un Producto Mínimo Viable (MVP) con un costo de implementación por hectárea significativamente menor a las soluciones industriales de grandes corporaciones, permitiendo un retorno de inversión (ROI) acelerado para el pequeño productor.

Después de un análisis profundo, estructurado bajo la técnica de las 5 ‘W’s y 2 ‘H’s, nos permitió identificar una brecha crítica en el sector agrícola: el distanciamiento entre la experiencia empírica del agricultor y la realidad de un entorno cada vez más hostil e impredecible. A través de este diagnóstico inicial, se determinó que los productores de pequeñas y medianas parcelas en Latinoamérica no solo enfrentan desafíos técnicos, sino una crisis de sostenibilidad económica y seguridad personal. Este mapeo preliminar reveló que la toma de decisiones basada exclusivamente en la intuición ha quedado obsoleta frente a factores que el ser humano no puede controlar a simple vista, como la variabilidad climática extrema y el aumento exponencial de la criminalidad rural.

Esta percepción diagnóstica se ve respaldada por datos locales alarmantes que sitúan al agro peruano en una de sus crisis más profundas de las últimas décadas. Según investigaciones de **Ojo Público (2023)**, el PBI del sector agropecuario sufrió una caída del 3.4% en el primer semestre de ese año, la cifra más crítica desde 1997, descapitalizando a los productores y limitando su capacidad de respuesta ante emergencias. Este escenario económico se entrelaza con un desafío global; **Pascoal et al. (2024)** señalan que el cambio climático ha vuelto imperativo el monitoreo en tiempo real de los ecosistemas mediante el Internet de las Cosas (IoT) para garantizar la seguridad alimentaria. Asimismo, especialistas como **Mishra et al. (2023)** subrayan que la gestión de la salud del suelo y el riego preciso son ya cuestiones de supervivencia operativa, mientras que revisiones de **Miller et al. (2025)** confirman que la integración de sensores inteligentes es el único camino para transitar de una agricultura reactiva a una de precisión.

Sin embargo, el problema identificado trasciende lo agronómico para convertirse en una crisis de seguridad patrimonial y humana. Al aplicar nuestra técnica de análisis, se detectó que el agricultor se encuentra en un estado de desprotección total frente a la delincuencia organizada. Datos de **Infobae (2026)** indican que la extorsión ya alcanza al 25% de los peruanos, expandiéndose agresivamente hacia las zonas rurales. La frecuencia de estos delitos es sobrecogedora: se registra una denuncia por extorsión cada 19 minutos en el país (**El Comercio, 2025**), y las proyecciones de víctimas mortales por sicariato y extorsión superan las 1,900 personas anualmente (**PQS, 2024**). Esta realidad convierte a los campos de cultivo en escenarios vulnerables donde el robo de insumos y la coacción criminal ocurren en la oscuridad, lejos de cualquier sistema de alerta inmediata.

Es por ello que dichos hallazgos revelan que la problemática de SATECHO quiere solventar va arraigado a la ineficiencia hídrica y la falta de datos técnicos que generan pérdidas de entre el 15% y 30% de la producción total. Por otro lado, la inseguridad ciudadana amenaza la continuidad misma de la actividad agrícola.
