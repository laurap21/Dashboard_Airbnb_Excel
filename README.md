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


# ⚙️ DESARROLLO DEL PROYECTO

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

## 🧠 Comprensión general de los datos 
Se ha hecho el análisis de dos archivos llamados “listings.csv” y "listings (1). csv" obtenidos de la web de datos abiertos de Airbnb. Finalmente, solo se utilizó uno de los dos archivos, ya que el primero contiene mayor información e incluye la del segundo archivo.

Se trata de un archivo de 79 columnas y 25.289 filas con información sobre los anfitriones (hosts) y sus anuncios de alojamientos en la ciudad de Madrid. Por lo tanto, se va a proceder a hacer **dos análisis**: uno sobre los hosts que tiene alojamientos en la Comunidad de Madrid y otro sobre los propios alojamientos. Se hará un cruce de datos para entender mejor el perfil del host.

## 🧹 Transformación y limpieza de los datos
### Eliminación de columnas irrelevantes
El archivo cuenta con **79 columnas**. Muchas de ellas han sido descartadas ya que no aportan valor real al análisis, como las columnas relativas al propio anuncio en la web (*listing_url*, *name*, *description*, *picture_url*, *host_url*, *host_name*, *host_thumbnail_url*, *host_picture_url*, *host_verifications*, *host_identity_verified*, etc.), así como las relativas a la puntuación en las *reviews* o valoraciónes, pues en este caso no se dispone de información suficiente sobre la forma de calificación empleada.

Finalmente, tras el análisis inicial de los datos, la tabla con los datos a analizar consta de **36 columnas**.

### Eliminación de filas irrelevantes para el análisis
El archivo cuenta con una columna denominada *source* que indica de dónde proviene el dato dentro del proceso de recolección. En este caso existen dos posibilidades "city scrape", que quiere decir que el dato fue extraído directamente de una web filtrada por ciudad, y "previous scrape", que indica que el dato fue recuperado o replicado de una búsqueda/recolección anterior, no de una búsqueda directa.

Por tanto, las filas correspondientes a "previous scrape" serán eliminadas, ya que se quiere hacer un análisis de la oferta actual de Airbnb.


### Tratamiento de datos: unificación de valores, eliminación de valores nulos y registros duplicados - Revisión de columnas.
Para la limpieza de los datos, se ha analizado columna a columna la calidad de los mismos realizando, según sea necesario, las siguientes actuaciones:
1. **Revisión de encabezados**: se corrigen los nombres de forma que queden más visuales y explicativos. 
2. **Revisión de valores duplicados**: 
    - No hay valores duplicados por anuncio (Primary Key). 
    - En cambio, por ID de Host sí hay, ya que un mismo host puede tener varios anuncios.
3. **Revisión de valores nulos/vacíos** :
    - La primera columna con valores nulos es *host_since*: existen valores vacíos que se van a eliminar, ya que no suponen una muestra de datos representativa frente al total (19 frente a 25.289, es decir, un 0,07 %). Además, se observa que estas filas tampoco disponen de información sobre el host.
    - Se han dejado casillas vacías en las columnas "Bedrooms", "Beds" y "Price_€" para el posterior análisis. Los datos vacíos de esta columna se tratarán más adelante como "no information" para las estadísticas de los anuncios.
4.	**Unificación de valores**: 
    - En la columna *host_location_initial* se observa gran variedad de localizaciones. El valor significativo para el análisis es solo el país, por lo que se crea la columna *Host_location* para unificar y limpiar los valores utilizando distintas fórmulas de Excel. En los valores en blanco se indica "Desconocido".
    - La columna *host_verification_initial* contiene información sobre los métodos de verificación de cada host. Se ha hecho una limpieza visual de los datos, eliminando los corchetes y las comillas y creando una nueva columna *Host_verification". También se ha añadido el valor "no verification" en las casillas vacías.
    - En la columna *Superhost* se ha incluido el valor "u" (unknown) para los espacios en blanco.
    - Se ha dividido el valor de la columna "Bathrooms" entre 10, de acuerdo a la explicación inicial de la columna en la que, por ejemplo, el valor 10 indica 1 baño y el valor 15 un baño y un aseo, es decir, 1,5 baños. Para mostrarlo, se ha creado la columna *Num. Bathrooms*.*
    - La columna *Bathrooms_text* amplía la información del número de baños indicando además si son compartidos o privados. En la columna *Shared_bathrooms* se ha extraído esta información complementaria.
    - En la columna *Price_€* se ha eliminado el símbolo del dólar, se ha reemplazado el punto por una coma y se ha específicado en el formato de la celda que son euros (€), ya que de acuerdo con la descripción de los datos esta corresponde a "daily price in local currency".
    - En la columna *Host_verifications* se han eliminado los corchetes y las comillas para dejar el texto más limpio. Se ha añadido el texto "no verifications" en las casillas vacías.

5. **Transformación a valores numéticos**
    - Para las columnas *Host_response_rate* y *Host_acceptance_rate* se han añadido dos columnas respectivas (*Host_response_rate_num* y *Host_acceptance_rate_num*) para transformar los datos disponibles a número para posibles futuros análisis. En estas columnas vienen mezclados valores de texto y valores que pueden ser numéricos. Las filas con valores en texto "N/A" se han dejado en blanco, transformando a número los distintos porcentajes que vienen en estas columnas.

6. **Revisión de valores atípicos y clasificación de valores en categorías. Hipótesis utilizadas.**
    - En las columnas relativas a las noches mínimas o máximas que permite el anfitrión se va a seguir el siguiente criterio:
        - En la columna *minimum_nights* se aceptan como valores válidos de 1 a 365. Los valores por encima de 365 se consideran atípicos. Se ha supuesto que el anfitrión hace uso de estos valores para bloquear la posibilidad de alquilar el alojamiento en el momento del scraping.
        Para analizar de manera más sencilla estos valores, tras la limpieza de los datos, se va a dividir según el número de noches mínimas en:

            | Num. Noches     | Categoría                 |
            |-----------------|---------------------------|
            | 1 - 3           | Very short stay           |
            | 4 - 7           | Short stay                |
            | 8 - 14          | Medium stay               |
            | 15 - 29         | Long stay                 |
            | 30 - 89         | Monthly rental            |
            | 90 - 365        | Extended temporary rental |
            | 365 o más       | Blocked rental            |


        - De igual manera, en la columna *maximum_nights* se consideran válidos los valores hasta 365. Los valores por encima de 365 se consideran atípicos. En este caso no van a ser eliminados, ya que se asume que el anfitrión ha elegido poner un número de noches máximas por encima del año para no limitar el alquiler de su alojamiento. Estos valores se utilizarán para suponer a qué tipo de alquiler está orientado el alojamiento:

            | Num. Noches     | Categoría                    |
            |-----------------|------------------------------|
            | 1 - 7           | Short stay only              |
            | 8 - 29          | Short to medium stay         |
            | 30 - 89         | Medium stay (up to 3 months) |
            | 90 - 365        | Long stay (up to 1 year)     |
            | 365 o más       | No real limit                |

    - De las diferentes opciones de disponibilidad del alojamiento, se va a emplear solamente la columna *availability_365* en este análisis. En función de la disponiblidad indicada en esta columna, se han creado las siguientes categorías:

        | Num. Noches     | Categoría             |
        |-----------------|-----------------------|
        | 0               | Not available         |
        | 1 - 89          | Low availability      |
        | 90 - 179        | Medium availability   |
        | 180 - 365       | High availability     |
        | 365 o más       | Fully available       |


El resto de columnas se ha eliminado del fichero, pues no se van a utilizar en este análisis porque no aportan información significativa o porque la información está incompleta.

Por otra parte, se han dejado casillas vacías en las columnas "Bedrooms", "Beds" y "Price_€" para el posterior análisis. Los datos vacíos de esta columna se tratarán más adelante como "no information" para las estadísticas de los anuncios.

Tras esta limpieza y transformación de los datos, se crea un fichero csv con el que posteriormente se trabajará.


# 📊 Análisis Descriptivo Hosts
Para el análisis del perfil de los Hosts o Anfitriones de Airbnb, se eliminan las columnas relativas a los Listings o Anuncios publicados.

Del datasheet filtrado y transformado de fases anteriores que contaba con todos los datos, se ha hecho un paso de transformación más, eliminando los *Host_ID* duplicados. Es decir, para el análisis del perfil de Hosts en Madrid se cuenta con un datasheet de 11 columnas y 7.896 filas.

## 🔢 Análisis de las variables numéricas
### **Host_response_rate_num**
Para el análisis de esta variable se ha de tener en cuenta que de los datos originales vienen muchas casillas en blanco, por lo que para el análisis de las variables estadísticas será necesario filtrarlas.

El total de valores en blanco de esta columna es igual a **903** que corresponde a un **11%** de los datos totales. Los **6.993 valores** restantes serán analizados:


# PRÓXIMOS PASOS PARA LAURA:
- Ver qué hacer con los outliers o cómo explicar la gran dispersión de mis datos.
- Ver cómo tratar los casos raros que no he visto antes: 15 baños para 2 personas (privado), etc.
- Revisar los histogramas y gráficas de los Excels de Análisis.

# LISTADO DE MÉTRICAS QUE QUIERO MOSTRAR EN MI ANÁLISIS
## HOSTS
- Número total de Hosts --> KPI Principal a mostrar
- Num. hosts con un solo anuncio.
- Hosts profesionales (a partir de 5 # listings, por ejemplo)
- % hosts verificados
- % superhosts
- Distribución medios de verificación
- Tiempo de respuesta --> Voy a usar el categórico
- % de aceptación --> Este ahora mismo no sé muy bien qué quiere decir.

## LISTINGS --> Análisis de la oferta
- Número total de listings --> KPI Principal a mostrar
- Distribución tipo de alojamiento
- Distribución tipo de habitación
- Distribución # huéspedes
- Distribución # baños
- Distribución # habitaciones
- Distribución # camas
- Distribución Precios general
- Tipo de alojamiento por barrio
- Precio por barrio
- Relación entre número de reseñas y precio --> los anuncios con precios entre 28 y 137 €/noche son los que más reseñas tienen. Precio más asequible. No sé si termina de tener sentido visual, igual en el análisis sí.

## MEZCLA CON LISTINGS: --> Segmentación de datos para el Dashboard (la gran mayoría)
- Superhosts vs no superhosts: diferencia de precios, disponibilidad, número de reviews
- Segmentación por barrios (precios, tipos de alojamiento, etc.)

## TIPS PARA CREAR EL DHASBOARD (de los vídeos de las clases):
1. "ctrl + k" --> Crear botón para cambio de Dashboards (cambio de pestañas) sin necesidad de crear Macros.
2. Crear segmentadores.
