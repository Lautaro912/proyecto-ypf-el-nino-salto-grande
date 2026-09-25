# ENSO y caudal en Salto Grande

Proyecto de Ciencia de Datos desarrollado en el marco de la formación de Fundación YPF — Grupo 13, Comisión 4.

## Descripción

Este proyecto explora la relación entre la variabilidad de ENSO —El Niño–Oscilación del Sur— y el caudal medio mensual registrado en Salto Grande Arriba, en la cuenca del río Uruguay.

La disponibilidad de agua es relevante para la generación hidroeléctrica. Comprender sus asociaciones con indicadores climáticos puede aportar antecedentes para futuras investigaciones orientadas a la planificación energética.

La primera entrega consiste en un análisis exploratorio de datos (EDA). No incluye un modelo predictivo ni una evaluación directa de la seguridad del suministro eléctrico.

## Pregunta de investigación

¿Qué asociaciones se observan entre los índices ONI, RONI y SOI y el caudal medio mensual registrado en Salto Grande Arriba durante 1996–2025?

## Objetivos

- Examinar la estructura, cobertura temporal y calidad de los datos.
- Identificar valores faltantes, duplicados y observaciones extremas.
- Describir la distribución y evolución temporal de cada variable.
- Explorar la estacionalidad del caudal y la autocorrelación de los índices.
- Analizar las asociaciones contemporáneas entre los índices y el caudal.

## Datos utilizados

| Dataset | Variable principal | Fuente |
|---|---|---|
| Salto Grande Arriba | Caudal medio mensual, en m³/s. Serie 24743, estación 77. | Instituto Nacional del Agua (INA) |
| ONI | Anomalía de temperatura superficial del mar en la región Niño 3.4, promediada en trimestres móviles. | NOAA Climate Prediction Center |
| RONI | Índice oceánico relativo que considera el contexto térmico de los océanos tropicales. | NOAA, archivo obtenido mediante PSL |
| SOI | Índice atmosférico mensual de Oscilación del Sur de Troup, adimensional. | Australian Bureau of Meteorology |

Fuentes de consulta:

- [Información hidrológica del INA](https://alerta.ina.gob.ar/)
- [Datos del ONI](https://www.cpc.ncep.noaa.gov/data/indices/oni.ascii.txt)
- [Información del RONI](https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso/roni/)
- [Series climáticas de NOAA PSL](https://psl.noaa.gov/data/timeseries/month/)
- [Datos mensuales del SOI](https://www.bom.gov.au/clim_data/IDCKGSH000/soi_monthly.txt)

La serie de Salto Grande se interpreta como caudal registrado en la estación. Su equivalencia con el aporte natural total al embalse no se considera verificada.

## Metodología

1. Inspección de dimensiones, tipos de datos, cobertura y duplicados.
2. Identificación de nulos, códigos de ausencia y meses sin registros.
3. Exploración individual mediante estadísticas descriptivas, series temporales, histogramas y boxplots.
4. Exploración del caudal por mes calendario.
5. Análisis de autocorrelación de los índices climáticos.
6. Integración por año y mes para el período 1996–2025.
7. Diagramas de dispersión y correlaciones de Pearson y Spearman.

Los dataframes originales se conservan sin modificaciones. Las transformaciones necesarias para la integración se realizan en estructuras auxiliares.

Los códigos de ausencia del RONI se excluyen de los cálculos y visualizaciones correspondientes. Los valores extremos no se eliminan automáticamente y los datos faltantes no se interpolan.

## Resultados preliminares

El análisis conjunto utiliza 359 meses con información completa de los 360 meses del período seleccionado.

Se observan asociaciones positivas del caudal con ONI y RONI, y negativas con SOI. Los diagramas muestran una dispersión considerable: valores similares de los índices pueden acompañarse de caudales diferentes.

Estos resultados son exploratorios. No demuestran causalidad, capacidad predictiva ni superioridad de un índice sobre otro.

## Limitaciones y verificaciones pendientes

- Confirmar la correspondencia entre las fechas del archivo RONI y sus períodos de cálculo.
- Considerar la estacionalidad del caudal y los posibles desfases temporales.
- Tener en cuenta la dependencia temporal de las observaciones al evaluar significancia estadística.
- Documentar las versiones y fechas de descarga de los datos.
- Corregir referencias a variables auxiliares no definidas y retirar bloques antiguos del notebook antes de validar su ejecución completa.

El ONI se referencia al mes central de su trimestre móvil. Esta asignación no lo convierte en una observación mensual independiente ni en información disponible en tiempo real durante ese mes.

No se incluyen datos de generación eléctrica, demanda ni operación del embalse; por lo tanto, no se cuantifican impactos sobre la seguridad energética.

## Notebook y ejecución

El análisis se desarrolla en `Propuesta_Proyecto_YPF.ipynb`, utilizando Python, pandas y Matplotlib en Google Colab.

Para trabajar con el notebook:

1. Abrirlo en Google Colab.
2. Montar Google Drive.
3. Ajustar la variable `carpeta` a la ubicación de los archivos.
4. Disponer de los siguientes archivos:
   - `salto_grande_arriba_24743_1995-2026.json`
   - `roni.csv`
   - `soi_monthly.txt`
5. Revisar las correcciones pendientes antes de ejecutar todas las celdas desde una sesión limpia.

El ONI se descarga desde NOAA durante la ejecución. Las actualizaciones de la fuente pueden modificar la cantidad de registros y los resultados.

## Próximos pasos

- Consolidar una versión reproducible del notebook.
- Verificar los metadatos y la alineación temporal.
- Evaluar las asociaciones considerando la estacionalidad.
- Explorar rezagos con una metodología explícita.
- Determinar si los datos justifican una etapa posterior de modelado predictivo.

## Referencias

- Timmermann et al. (2018). *El Niño–Southern Oscillation complexity*. Nature. https://doi.org/10.1038/s41586-018-0252-6
- Santoso, McPhaden y Cai (2017). *The Defining Characteristics of ENSO Extremes and the Strong 2015/2016 El Niño*. Reviews of Geophysics. https://doi.org/10.1002/2017RG000560
- Levine y McPhaden (2015). *The annual cycle in ENSO growth rate as a cause of the spring predictability barrier*. Geophysical Research Letters. https://doi.org/10.1002/2015GL064309
2:59 p.m.
