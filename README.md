[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Lautaro912/proyecto-ypf-el-nino-salto-grande/blob/main/Propuesta_Proyecto_YPF.ipynb)

# ENSO y caudal mensual en Salto Grande

Proyecto de Ciencia de Datos desarrollado en el marco de la formación de **Fundación YPF — Grupo 13, Comisión 4**.

**Integrantes:** Francisco Quarin y Lautaro Moya.

## Descripción del proyecto

Este proyecto analiza la relación entre la variabilidad de ENSO —El Niño–Oscilación del Sur— y el caudal medio mensual registrado en Salto Grande Arriba, en la cuenca del río Uruguay.

ENSO es un fenómeno de interacción entre el océano y la atmósfera del Pacífico tropical. Sus fases se relacionan con cambios en la circulación atmosférica y pueden influir en los patrones de precipitación de distintas regiones. La disponibilidad de agua resulta relevante para la generación hidroeléctrica, por lo que estudiar su relación con indicadores climáticos puede aportar información para futuras investigaciones sobre planificación energética.

El trabajo utiliza tres índices climáticos —ONI, RONI y SOI— y una serie de caudal del Instituto Nacional del Agua (INA).

El notebook desarrolla tres líneas de análisis:

1. **Análisis exploratorio de datos (EDA):** revisión de calidad, cobertura, distribuciones, evolución temporal, estacionalidad y dependencia temporal.
2. **Modelado supervisado:** evaluación de modelos lineales para estimar anomalías mensuales de caudal a horizontes de uno y tres meses.
3. **Aprendizaje no supervisado:** aplicación de K-Means para explorar agrupamientos retrospectivos de condiciones climáticas e hidrológicas.

El objetivo es estudiar asociaciones y evaluar alternativas analíticas. El proyecto no predice directamente la generación eléctrica ni constituye una herramienta operativa de despacho energético.

## Pregunta de investigación

¿Qué relación existe entre los índices ONI, RONI y SOI y el comportamiento del caudal mensual registrado en Salto Grande Arriba? ¿En qué medida estos indicadores, combinados o por separado, aportan información para estimar anomalías de caudal a uno y tres meses?

## Objetivos

### Objetivo general

Analizar la relación entre indicadores de ENSO y el caudal mensual de Salto Grande Arriba mediante técnicas de análisis exploratorio, modelado supervisado y aprendizaje no supervisado.

### Objetivos específicos

- Documentar las fuentes, variables, unidades y coberturas temporales.
- Examinar la calidad de los datos e identificar valores ausentes, códigos de ausencia, duplicados y discontinuidades.
- Describir las distribuciones y la evolución temporal de las variables.
- Explorar la estacionalidad del caudal y la dependencia temporal de los índices.
- Analizar las asociaciones contemporáneas entre ONI, RONI, SOI y caudal.
- Construir y evaluar modelos supervisados para estimar anomalías de caudal a uno y tres meses.
- Comparar el aporte de la información climática con referencias basadas en climatología y persistencia.
- Explorar agrupamientos de condiciones climáticas e hidrológicas mediante K-Means.
- Identificar limitaciones y oportunidades de mejora para futuras investigaciones.

## Datos utilizados

| Serie | Variable principal | Fuente |
|---|---|---|
| Salto Grande Arriba | Caudal medio mensual (m³/s), serie 24743, estación 77 | Instituto Nacional del Agua (INA) |
| ONI | Anomalía de temperatura superficial del mar en la región Niño 3.4, calculada mediante trimestres móviles | NOAA Climate Prediction Center |
| RONI | Índice oceánico relativo de El Niño | NOAA / archivo obtenido mediante PSL |
| SOI | Índice mensual de Oscilación del Sur de Troup | Australian Bureau of Meteorology |

El análisis conjunto exploratorio utiliza el período **1996–2025**. En los resultados guardados de esa etapa se utilizaron 359 meses completos de los 360 meses calendario del período.

La cobertura individual de cada fuente es más amplia y no debe confundirse con el período común utilizado para integrar las series.

## Metodología

### 1. Preparación y exploración de los datos

Se utilizaron Python, pandas y Matplotlib para cargar e inspeccionar las cuatro series. Se revisaron dimensiones, tipos de datos, valores faltantes, duplicados, cobertura temporal y distribuciones.

Se prestó especial atención a los códigos de ausencia presentes en el archivo RONI, ya que un valor codificado numéricamente no necesariamente es reconocido por pandas como dato nulo.

### 2. Análisis exploratorio

Se analizaron las series temporales, distribuciones, valores extremos y comportamiento mensual del caudal. También se examinó la autocorrelación de los índices climáticos para reconocer su dependencia temporal.

### 3. Integración y asociaciones

Las series se integraron mediante referencias temporales de año y mes. Se exploraron asociaciones contemporáneas con diagramas de dispersión y correlaciones de Pearson y Spearman.

Estas correlaciones son descriptivas: no representan porcentajes de caudal explicado ni permiten establecer causalidad.

### 4. Modelado supervisado

Se evaluaron modelos lineales OLS y Ridge para estimar anomalías mensuales de caudal a horizontes de uno y tres meses.

La evaluación utiliza particiones cronológicas para respetar el orden temporal. Se comparan modelos con información ENSO, información hidrológica rezagada y combinaciones de ambas. También se consideran referencias de climatología y persistencia.

El conjunto de prueba se reserva para la evaluación final, con orígenes desde enero de 2020, según la metodología documentada en las conclusiones del notebook.

### 5. Aprendizaje no supervisado

Se implementa K-Means con variables climáticas rezagadas y anomalías mensuales de caudal. Se incorpora escalado previo y evaluación de distintos valores de k mediante inercia y Silhouette.

Este análisis es retrospectivo: al utilizar información del caudal observado para formar los grupos, no debe interpretarse como un sistema de predicción anticipada.

## Resultados

### Análisis exploratorio

En los resultados guardados del análisis conjunto se observan las siguientes asociaciones contemporáneas:

| Índice | Pearson | Spearman |
|---|---:|---:|
| ONI | 0,495 | 0,370 |
| RONI* | 0,488 | 0,355 |
| SOI | −0,298 | −0,247 |

\*La alineación temporal del RONI se considera provisional y requiere verificación de sus metadatos.

Los coeficientes muestran asociaciones positivas entre caudal y ONI/RONI, y negativas entre caudal y SOI. La dispersión de los datos indica que valores similares de los índices pueden acompañarse de caudales diferentes.

### Modelado supervisado

La sección de conclusiones finales del notebook informa los siguientes resultados para los modelos seleccionados mediante validación cruzada:

| Horizonte | Modelo seleccionado | MAE de Test (m³/s) | RMSE de Test (m³/s) | R² de Test |
|---|---|---:|---:|---:|
| 1 mes | ENSO + hidrológico — Ridge α=100 | 2627,62 | 3598,43 | 0,264 |
| 3 meses | ENSO — Ridge α=100 | 2979,86 | 3930,24 | 0,137 |

En esa misma sección se informa una reducción del MAE respecto de la referencia climatológica de aproximadamente 20,9 % para un mes y 10,7 % para tres meses.

La comparación con modelos hidrológicos muestra que la mejora atribuible a incorporar ENSO es pequeña en la validación cruzada. Por lo tanto, estos resultados no demuestran de manera concluyente que los índices climáticos aporten una mejora incremental robusta frente a la información hidrológica disponible.

Los valores anteriores corresponden a los resultados consignados en las conclusiones finales del notebook y deben contrastarse con una ejecución completa y reproducible de la versión definitiva.

### Aprendizaje no supervisado

El notebook incluye una implementación de K-Means para explorar agrupamientos de condiciones climáticas e hidrológicas. Los valores finales de k, Silhouette y los perfiles de los grupos deben obtenerse y revisarse a partir de la ejecución completa de esa sección. No se presentan aquí como resultados numéricos confirmados.

## Limitaciones

- La equivalencia entre el caudal registrado en la estación y el aporte natural total al embalse no está verificada.
- La alineación temporal del RONI requiere confirmar documentalmente sus ventanas de cálculo.
- ONI utiliza trimestres móviles, mientras que el caudal y SOI tienen resolución mensual; compartir una etiqueta de mes no significa que las ventanas temporales sean equivalentes.
- Las correlaciones exploratorias no ajustan por estacionalidad ni dependencia temporal.
- Los resultados predictivos dependen del período de entrenamiento, de prueba y de la disponibilidad efectiva de los índices.
- Deben verificarse las fechas de publicación y las revisiones históricas de ONI, RONI y SOI antes de interpretar los pronósticos como información que habría estado disponible en tiempo real.
- La evaluación no demuestra causalidad.
- No se incluyen datos de generación eléctrica, demanda ni operación del embalse. Por eso no se cuantifican impactos sobre el despacho ni sobre la seguridad del suministro eléctrico.
- Los resultados de K-Means deben verificarse con la ejecución completa de la sección correspondiente.

## Cómo ejecutar el notebook

El análisis se desarrolla en `Propuesta_Proyecto_YPF.ipynb` mediante Python y Google Colab.

Para ejecutarlo:

1. Abrir el notebook en Google Colab.
2. Montar Google Drive.
3. Ajustar la variable `carpeta` a la ubicación de los archivos.
4. Disponer de los siguientes archivos:
   - `salto_grande_arriba_24743_1995-2026.json`
   - `roni.csv`
   - `soi_monthly.txt`
5. Ejecutar las celdas en orden desde una sesión limpia.
6. Verificar que los resultados recalculados coincidan con las conclusiones documentadas.

El ONI se obtiene desde NOAA durante la ejecución, por lo que las actualizaciones de la fuente pueden modificar los registros y resultados.

## Próximos pasos

- Consolidar una única versión del notebook y retirar bloques históricos o conclusiones que hayan quedado desactualizados.
- Verificar la alineación temporal del RONI y los metadatos de la serie hidrológica.
- Reproducir los resultados desde una sesión limpia.

## Referencias

- Timmermann et al. (2018). *El Niño–Southern Oscillation complexity*. Nature. https://doi.org/10.1038/s41586-018-0252-6
- Santoso, McPhaden y Cai (2017). *The Defining Characteristics of ENSO Extremes and the Strong 2015/2016 El Niño*. Reviews of Geophysics. https://doi.org/10.1002/2017RG000560
- Levine y McPhaden (2015). *The annual cycle in ENSO growth rate as a cause of the spring predictability barrier*. Geophysical Research Letters. https://doi.org/10.1002/2015GL064309
2:59 p.m.
