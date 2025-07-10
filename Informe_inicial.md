# 🏡 Análisis de Datos Abiertos de Airbnb en Madrid

![](https://media.licdn.com/dms/image/v2/D4E12AQFZ4xlAbu0NAw/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1712840717484?e=1757548800&v=beta&t=l2jH7-D-Ht4BVTWy-JEyV_f6QGzIam_zk2b_pRF0iLc)

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