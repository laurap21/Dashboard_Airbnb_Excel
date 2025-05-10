# 🏡 Análisis de Datos Abiertos de Airbnb en Madrid
Curso: Data Analytics V3 | Proyecto: Dashboard &amp; Análisis de Datos

Este proyecto tiene como objetivo analizar los datos abiertos de Airbnb en la ciudad de Madrid. A lo largo del proyecto se realiza una transformación y limpieza de datos, análisis descriptivo, creación de un dashboard interactivo y elaboración de un informe explicativo con las principales conclusiones.


![](https://media.licdn.com/dms/image/v2/D4E12AQFZ4xlAbu0NAw/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1712840717484?e=1752105600&v=beta&t=l8uX2liBFQ_GU1obAcE0mTau9cKQWacMdBHiz2UZy6U)

## 📄 INFORME INICIAL

### 1. Contexto y Problema Actual 🚩
La Comunidad de Madrid está experimentando una creciente preocupación en relación con el impacto del alquiler vacacional en el acceso a la vivienda y el desarrollo urbano. En este contexto, se ha solicitado un análisis basado en datos abiertos de la plataforma Airbnb, con el fin de comprender mejor el comportamiento de los principales anfitriones y la oferta actual de alojamientos turísticos.

Este análisis busca responder a preguntas clave como:

- ¿Quiénes son los principales anfitriones y cuántos alojamientos gestionan?

- ¿Qué tipo de propiedades se ofrecen como alquiler vacacional en Madrid?

- ¿En qué zonas se concentra la actividad de Airbnb?

Para facilitar la toma de decisiones informadas por parte de las autoridades y los agentes implicados, se propone el desarrollo de una herramienta visual que permita explorar y actualizar esta información de forma sencilla y en tiempo real.

### 2. Objetivo principal del proyecto 🎯
El propósito de este proyecto es diseñar y construir uno o varios **dashboards interactivos** que permitan:

- **Identificar el perfil genérico del anfitrión**, incluyendo características como su localización, número de anuncios gestionados, tipo de anfitrión (profesional o particular), etc.

- **Analizar la oferta actual de alojamientos vacacionales en la ciudad de Madrid**, considerando atributos como tipo de propiedad, precios, localización geográfica, disponibilidad y valoraciones de los usuarios.

Estos dashboards actuarán como una herramienta de análisis dinámica para responsables públicos, investigadores y otros interesados en el fenómeno del alquiler vacacional.

### 3. Descripción del Conjunto de Datos 🔗

El conjunto de datos utilizado en este proyecto ha sido extraído de la plataforma [Inside Airbnb](https://insideairbnb.com/get-the-data/), que proporciona datos abiertos y actualizados sobre la actividad de Airbnb en distintas ciudades del mundo. La explicación de todas las columnas viene en el siguiente enlace: [Descripción Columnas](https://docs.google.com/spreadsheets/d/1b_dvmyhb_kAJhUmv81rAxl4KcXn0Pymz/edit?gid=1967362979#gid=1967362979)

En el caso de Madrid, los datos se organizan en varias tablas, siendo las principales:

#### a. Datos de los anfitriones
Incluye la siguiente información:
- *host_id*: Identificador del anfitrión.
- *host_name*: Nombre del anfitrión.
- *host_since*: Fecha de alta en la plataforma.
- *host_listings_count*: Número total de anuncios gestionados.
- *host_is_superhost*: Si el anfitrión tiene la categoría de "superhost".
- *host_location*: Ciudad o país declarado.
- Otros atributos de comportamiento (e.g., tasa de respuesta, idioma del perfil, etc.).

#### b. Datos de los alojamientos
Contiene variables como: 
- *id*: Identificador del anuncio.
- *name*: Título del alojamiento.
- *neighbourhood*: Barrio o zona dentro de Madrid.
- *room_type*: Tipo de alojamiento (habitación privada, apartamento entero, etc.).
- *price*: Precio por noche.
- *availability_365*: Días disponibles al año
- *number_of_reviews*: Número de valoraciones recibidas
- *review_scores_rating*: Puntuación media del alojamiento

### 4. Próximos Pasos ⏭️
A continuación se detallan las etapas previstas para el desarrollo del proyecto:

- **Recepción y validación de los datos completos**: Asegurar que los archivos están actualizados, completos y correctamente estructurados.

- **Análisis Exploratorio de Datos (EDA)**: Examinar los datos para identificar patrones, valores atípicos, valores nulos o inconsistencias. Generar visualizaciones preliminares para comprender la estructura de los datos.

- **Diseño de Dashboards**: Crear dashboards interactivos en Excel que representen las métricas clave relacionadas con anfitriones y alojamientos.

- **Presentación de Resultados**: Entregar un informe final con las conclusiones extraídas, visualizaciones relevantes e hipótesis explicativas. Incluir recomendaciones para futuras políticas o investigaciones.

## 📁 ESTRUCTURA DEL PROYECTO
```
📂 Dashboard_Airbnb_Excel
├── Datasets/
│   └── Datasets Airbnb Madrid.xlxs   # Datos brutos descargados de Inside Airbnb
│   └── Dasets Ejemplo.xlsx           # Datos brutos descargados de Inside Airbnb
├── Datos iniciales/
│   └── listings.csv                  # Datos originales 
│   └── listings (1).csv              # Datos originales (1)
├── Excel/
│   └── Airbnb Madrid Completo.xlsx   # Archivo de trabajo (EDA, Dashboards)
├── Proyecto_Airbnb_Madrid.docx       # Documento inicial de trabajo
└── README.md
```

## ⚙️ DESARROLLO DEL PROYECTO

### 🧠 1. Comprensión general de los datos 
Se ha hecho el análisis de dos archivos llamados “listings.csv” y "listings (1). csv" obtenidos de la web de datos abiertos de Airbnb. Finalmente, solo se utilizó uno de los dos archivos, ya que el primero contiene mayor información e incluye la del segundo archivo.

Se trata de un archivo de 79 columnas y 25.289 filas con información sobre los anfitriones (hosts) y sus anuncios de alojamientos en la ciudad de Madrid. Por lo tanto, se va a proceder a hacer **dos análisis**: uno sobre los hosts que tiene alojamientos en la Comunidad de Madrid y otro sobre los propios alojamientos. Se hará un cruce de datos para entender mejor el perfil del host.

### 🧹 2. Transformación y limpieza de los datos
#### Eliminación de columnas irrelevantes
El archivo cuenta con **79 columnas**, de las cuales se van a emplear **X**. El resto han sido descartadas ya que no aportan valor real al análisis, como las columnas relativas al propio anuncio en la web (*listing_url*, *name*, *description*, *picture_url*, *host_url*, *host_name*, *host_thumbnail_url*, *host_picture_url*, *host_verifications*, *host_identity_verified*, etc.).

Finalmente, tras el análisis inicial de los datos, la tabla con los datos a analizar consta de **X columnas**.


#### Tratamiento de datos: unificación de valores, eliminación de valores nulos y registros duplicados
1. **Revisión de encabezados**: se incluyen notas aclaratorias de los encabezados necesarios. También se corrigen los nombres de forma que queden más visuales y explicativos. 
2. **Revisión de valores duplicados**: 
    - No hay valores duplicados por anuncio (Primary Key). 
    - En cambio, por ID de Host sí hay, ya que un mismo host puede tener varios anuncios.
3. **Revisión de valores nulos** :
    - La primera columna con valores nulos es *host_since*: existen valores nulos que se van a eliminar, ya que no suponen una muestra de datos representativa frente al total (19 frente a 25.289, es decir, un 0,07 %). Además, se observa que estas filas tampoco disponen de información sobre el host.
4.	**Unificación de valores**: 
    - En la columna *host_location* se observa gran variedad de localizaciones. El valor significativo para el análisis es solo el país, por lo que se crea la columna *Host_location2* para unificar y limpiar los valores utilizando distintas fórmulas de Excel. En los valores en blanco se indica "Desconocido".
    - De igual manera, en la columna **Superhost** se ha incluido el valor "d" (desconocido) para los espacios en blanco.


#### Filtros por disponibilidad y tipo de alojamiento