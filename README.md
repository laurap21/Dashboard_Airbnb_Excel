# 🏡 Análisis de Datos Abiertos de Airbnb en Madrid
Curso: Data Analytics V3 | Proyecto: Dashboard &amp; Análisis de Datos

## DESCRIPCIÓN DEL PROYECTO 

Este proyecto tiene como objetivo analizar los datos abiertos de Airbnb en la ciudad de Madrid. A lo largo del proyecto se realiza una transformación y limpieza de datos, análisis descriptivo, creación de un dashboard interactivo y elaboración de un informe explicativo con las principales conclusiones.

El informe inicial con el problema de análisis planteado es el siguiente: [Informe Inicial](Informe_inicial.md)

El principal objetico es crear de forma visual un perfil de *Hosts* (anfitriones) y *Listings* (anuncios) en Madrid para entender la situación actual.

## 📁 ESTRUCTURA DEL PROYECTO
```
📂 Dashboard_Airbnb_Excel
├──Data/
│   └── Airbnb Madrid Completo_Dashboards.xlxs   # Archivo con los dashboards finales
│   └── Airbnb_Madrid_Analisis_Hosts.xlsx        # Análisis de los datos de los Hosts
│   └── Airbnb_Madrid_Analisis_Listings.xlsx     # Análisis de los datosde los los Listings
│   └── Airbnb Madrid Completo_V3.csv            # Archivo .csv de datos filtrados sobre el que hacer los análisis
│   └── OLD/                                     # Versiones antiguas descartadas
│       └── Airbnb Madrid Completo_V1.csv
│       └── Airbnb Madrid Completo_V2.csv
│       └── Airbnb_Madrid_Analisis.xlsx
│       └── Airbnb_Madrod_Analisis_V2.xlsx
│       └── Airbnb_Madrod_Analisis_V3.xlsx
├──Datasets/
│   └── Datasets Airbnb Madrid.xlxs              # Datos brutos descargados de Inside Airbnb
│   └── Dasets Ejemplo.xlsx                      # Datos brutos descargados de Inside Airbnb
├── Datos iniciales/
│   └── listings.csv                             # Datos originales 
│   └── listings (1).csv                         # Datos originales (1)
├── Excel/
│   └── Airbnb Madrid Completo.xlsx              # Archivo de trabajo (EDA, Dashboards)
│   └── Airbnb Madrid Completo_V1.xlsx           # Archivo de trabajo (EDA, Dashboards) - V1 solventando errores
├── Images/
├── Informe_analisis.md                          # Archivo .md con el informe del análisis
├── Informe_inicial.md                           # Archivo .md con el problema para análisis
└── README.md
```

## 🔗 FUENTE DE DATOS

El conjunto de datos utilizado en este proyecto ha sido extraído de la plataforma [Inside Airbnb](https://insideairbnb.com/get-the-data/), que proporciona datos abiertos y actualizados sobre la actividad de Airbnb en distintas ciudades del mundo. La explicación de todas las columnas viene en el siguiente enlace: [Descripción Columnas](https://docs.google.com/spreadsheets/d/1b_dvmyhb_kAJhUmv81rAxl4KcXn0Pymz/edit?gid=1967362979#gid=1967362979)

## 🧹 TRANSFORMACIÓN Y LIMPIEZA

Para el correcto análisis de los datos se ha llevado a cabo un proceso de transformación y limpieza. El archivo inciial empleado contenía 79 columnas y 25.289 filas con información sobre los anfitriones (hosts) y sus anuncios de alojamientos en la ciudad de Madrid. Finalmente, tras el proceso, el archivo a analizar cuenta con 36 columnas y 19.274 filas.

Las transformaciones realizadas han sido las siguientes, más detalladas en el informe del proyecto:
- Eliminación de columnas irrelevantes.
- Eliminación de filas irrelevantes para el análisis, es decir, con errores o valores nulos en las columnas finales.
- Tratamiento de datos: unificación de valores, eliminación de nulos y registros duplicados, revisión general de columnas.

## 📊 ANÁLISIS DESCRIPTIVO

El análisis se ha dividido en dos: un análisis para el perfil de hosts y otro para el perfil de listings. 

En ambos casos se han analizado todas las variables, tanto numéricas como categóricas, así como un breve análisis bivariable de las características que podrían mostrar algún tipo de correlación (de acuerdo a la matriz de correlaciones generada). 

## 📈 DASHBOARD INTERACTIVO

Dada la cantidad de datos y de información disponible, y teniendo en cuenta el objetivo de mostrar visualmente dos perfiles (hosts y listings), se han realizado dos dashboards interactivos en los que se muestran:

1. **Dashboard General:** 
Dividido en dos columnas no simétricas, se muestra a la izquiera el perfil de los hosts y a la izquierda el perfil general de los listings. En el centro se muestran los principales KPIs para cada grupo de análisis.
    -  Para el perfil de los Hosts: el KPI principal es el número total de Hosts disponibles, así como los que se consideran SuperHosts y los que están verificados por la plataforma. En cuanto a los segmentadores empleados para crear filtros, en este caso se consideran: *superhost*, *verified host* y *host response time* (tiempo de respuesta). En las gráficas se ve el reparto del total de listings por host (variable fija, no afectada por los segmentadores) que indica que casi la mitad de los hosts tiene entre 1 y 5 listings (considerandose como actividad no profesional), los medios de verificación activados por el anfitrión, el tiempo de respuesta del mismo y la ubicación (mostrada en un mapa).
    - Por otro lado, para el perfil de los listings, los KPIs principales son el número total de anuncios publicados, el precio medio y el número medio de reseñas. Se muestra también un gráfico con la distribución por distrito dentro de Madrid, ya que es la variable principal para segmentar estos datos (que también afecta al perfil del host). Las principales gráficas mostradas en este perfil son: promedio de número de huéspedes, de número de baños y de número de camas; perfil del tipo de habitación, de baños compartidos y de la disponibilidad o no de reserva automática, la distribución de precios y de disponibilidad anual. En este caso, la segmentación principal se hace por distrito (quedando en el centro del dashboard).


2. **Dashboards listings**:
En este dashboard se muestra de forma más específica el perfil de los anuncios:
    - En el lateral izquierdo se muestran los principales KPIs mencionados para el dashboard anterior, la gráfica de distribución de listings por distrito y la segmentación por distritos.
    - En cuanto a la descripción del perfil se muestra lo siguiente: 
        - La distribución del tipo de habitación.
        - La disponibilidad anual.
        - La distribución del número de huéspedes.
        - La distribución del número de baños y si son compartidos o no.
        - La disponibilidad de reserva automática.
        - La distribución de precios.
        - El número mínimo de noches categorizado en: estancias muy cortas, estancias cortas, estancias medias, estancias largas, alquileres mensuales, alquileres temporales largos y alquileres bloqueados.

Se puede acceder a ambos dashboards desde el otro con el botón situado arriba a la derecha.

## 📄 INFORME FINAL

El informe final del proyecto incluye la descripción detallada de la limpieza y transformación de datos, así como el análisis completo de las variables numéricas y categóricas de los *hosts* y de los *listings*. Para ambos casos también se incluye una descripción del análisis vibariable considerado más relevante. 

## 💻 HERRAMIENTAS UTILIZADAS
El análisis descriptivo se ha realizado empleando las herramientas estadísticas y de visualización proporcionadas por **Microsoft Excel**.

## ✅ RESULTADOS Y CONCLUSIONES
Aproximadamente la mitad de los anfitriones no tiene como fuente principal de ingresos Airbnb ya que cuentan con entre 1 y 5 alojamientos disponibles. Para verificar esta hipótesis se deberá, en próximos pasos, comprobar con la disponibilidad de los anuncios que tienen si son estacionales o están disponibles durante largos periodos de tiempo en el año. 
Por otro lado, los anfitriones suelen responder de forma rápida y cómoda, por correo electrónico o teléfono, mejorando así la experiencia del usuario. 

En cuanto a los anuncios, el perfil de alojamiento está orientado a parejas o grupos pequeños de hasta 5 personas, de acuerdo con el número de camas o habitaciones disponibles. El número de baños más recurrente es 1, corroborando la afirmación anterior. Las anuncios se inclinan hacia estancias de corta duración. Con respecto a los precios, varían mucho en función del distrito y de las características físicas (camas, baños, etc.), siendo el valor promedio de 138,89€.

## ➡️ PRÓXIMOS PASOS
- Profundizar en el análisis del perfil de alojamientos por distrito, considerando el número de huéspedes, baños, precio y número de habitaciones.
- Cruzar la información de los hosts "profesionales" con las características de sus anuncios para verificar las hipótesis realizadas.
- Revisión de los datos iniciales con respecto a las reseñas.


## 👩🏼‍💻 AUTORES Y AGRADECIMIENTOS
Este proyecto ha sido desarrollado enteramente por Laura Pomares Bleda como parte del curso **Data Analytics V3**. 
Fecha de entrega: Julio 2025.
