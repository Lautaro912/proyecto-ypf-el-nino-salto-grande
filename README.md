# **Fundacion YPF - Formación en Ciencia de Datos**

# *Grupo 13 - Comision 4*

> Francisco Quarin

> Lautaro Moya

# **Impacto en la Energía**

Análisis del impacto de El Niño (ENOS) en el caudal afluente (inflow) de Salto Grande y su relación con la seguridad energética nacional.

Explico lo que por el momento vi en clase de **ENSO (El Niño-Oscilación del Sur)** y por que lo propongo en este proyecto.


# Introducción:

`¿Cómo se conecta el Océano con la energía de nuestras casas? `

Para entender este proyecto, imaginemos que el Océano Pacífico es como la batería térmica gigante del planeta. Gracias a que el agua tiene un "calor específico" altísimo (le cuesta mucho calentarse y enfriarse), el océano absorbe más del 90% del exceso de calor global. Por eso decimos que el océano es la memoria del clima, es decir, mientras la atmósfera cambia de opinión de un día para el otro, el océano almacena y "recuerda" la energía durante meses.

Cuando los vientos globales (vientos alisios) se debilitan, esa inmensa masa de agua caliente acumulada en Asia viaja de regreso hacia Sudamérica. A este calentamiento lo conocemos como el Fenómeno de El Niño (ENOS). Este cambio térmico altera por completo las nubes y las lluvias en nuestro continente, provocando sequías históricas en las zonas donde están ubicadas las represas hidroeléctricas.

Seguimos...

El **ENSO (El Niño-Oscilación del Sur)** es el ejemplo perfecto de un fenómeno acoplado entre dos fluidos, lo que quiere decir, es que en condiciones normales esos vientos alisios soplan con fuerza de este a oeste, acumulando agua cálida en el Pacífico occidental (cerca de Asia).
Durante El Niño, los vientos alisios se debilitan. Al no haber viento que empuje el agua hacia el oeste, la masa de agua cálida del Pacífico central y occidental fluye de regreso hacia las costas de Sudamérica (Perú, Colombia, Ecuador)

Entonces, el Océano actua como regulador térmico del planeta, nuestro punto entonces es... explicar por qué nos importa tanto esto en el balance de energía terrestre, por que a traves de vincular la dinámica física de la Tierra (la interacción atmósfera-océano y el calor específico del agua) con la gestión hidroeléctrica es la definición perfecta de un proyecto de impacto real y productivo. Además, el programa valora especialmente que el proyecto "cuente una historia con los datos".

Pregunta a responder:

¿Cómo se relacionan las variaciones de ENSO con las anomalías del caudal medio mensual afluente al embalse de Salto Grande, y cómo cambia esta relación según la época del año y los posibles desfases temporales?

# Objetivo :

> Lo que haríamos sería...desarrollar un modelo de Machine Learning que cruce los datos de temperatura del Océano Pacífico (de la NOAA) con los registros de lluvia de las estaciones terrestres (del SMN), para predecir con meses de anticipación cuánta agua entrará naturalmente (inflow) a las represas hídricas clave.


> **¿Para qué sirve?** Si nuestro modelo detecta que el caudal va a caer drásticamente por culpa de El Niño, se genera una alerta temprana para CAMMESA. Así, el sistema eléctrico nacional puede programar con tiempo el encendido de centrales termoeléctricas de respaldo, las cuales consumen el gas y combustible que produce YPF, evitando apagones y optimizando los recursos del país.
