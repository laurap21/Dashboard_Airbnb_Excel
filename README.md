# 🏡 Análisis de Datos Abiertos de Airbnb en Madrid
Curso: Data Analytics V3 | Proyecto: Dashboard &amp; Análisis de Datos

Este proyecto tiene como objetivo analizar los datos abiertos de Airbnb en la ciudad de Madrid. A lo largo del proyecto se realiza una transformación y limpieza de datos, análisis descriptivo, creación de un dashboard interactivo y elaboración de un informe explicativo con las principales conclusiones.

El informe inicial con el problema de análisis planteado es el siguiente: [Informe Inicial](Informe_inicial.md)



# ⚙️ DESARROLLO DEL PROYECTO

## 📁 ESTRUCTURA DEL PROYECTO
```
📂 Dashboard_Airbnb_Excel
├──Data/
│   └── Airbnb Madrid Completo_Dashboards.xlxs   # Archivo con los dashboards finales
│   └── Airbnb_Madrid_Analisis_Hosts.xlsx        # Análisis de los datos de los Hosts
│   └── Airbnb_Madrid_Analisis_Listings.xlsx     # Análisis de los datosde los los Listings
│   └── OLD/                                     # Versiones antiguas descartadas
│       └── Airbnb Madrid Completo_V1.csv
│       └── Airbnb Madrid Completo_V2.csv
│       └── Airbnb Madrid Completo_V3.csv
│       └── Airbnb_Madrid_Analisis.xlsx
│       └── Airbnb_Madrod_Analisis_V2.xlsx
│       └── Airbnb_Madrod_Analisis_V3.xlsx
├──Datasets/
│   └── Datasets Airbnb Madrid.xlxs   # Datos brutos descargados de Inside Airbnb
│   └── Dasets Ejemplo.xlsx           # Datos brutos descargados de Inside Airbnb
├── Datos iniciales/
│   └── listings.csv                  # Datos originales 
│   └── listings (1).csv              # Datos originales (1)
├── Excel/
│   └── Airbnb Madrid Completo.xlsx   # Archivo de trabajo (EDA, Dashboards)
│   └── Airbnb Madrid Completo_V1.xlsx   # Archivo de trabajo (EDA, Dashboards) - V1 solventando errores
├── Proyecto_Airbnb_Madrid.docx       # Documento inicial de trabajo
├── Informe_inicial.md                # Archivo .md con el problema para análisis
└── README.md
```

## 🧠 Comprensión general de los datos 
Se ha hecho el análisis de dos archivos llamados “listings.csv” y "listings (1). csv" obtenidos de la web de datos abiertos de Airbnb. Finalmente, solo se ha utilizado uno de los dos archivos, ya que el primero contiene mayor información e incluye la del segundo archivo.

Se trata de un archivo de 79 columnas y 25.289 filas con información sobre los anfitriones (hosts) y sus anuncios de alojamientos en la ciudad de Madrid. Por lo tanto, se va a proceder a hacer **dos análisis**: uno sobre los hosts que tiene alojamientos en la Comunidad de Madrid y otro sobre los propios alojamientos.

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
    - Se han dejado casillas vacías en las columnas "Bedrooms", "Beds" y "Price_€" para el posterior análisis.
4.	**Unificación de valores**: 
    - En la columna *host_location_initial* se observa gran variedad de localizaciones. El valor significativo para el análisis es solo el país, por lo que se crea la columna *Host_location* para unificar y limpiar los valores utilizando distintas fórmulas de Excel. En los valores en blanco se indica "Unknown".
    - La columna *host_verification_initial* contiene información sobre los métodos de verificación de cada host. Se ha hecho una limpieza visual de los datos, eliminando los corchetes y las comillas y creando una nueva columna *Host_verification*. También se ha añadido el valor "no verification" en las casillas vacías.
    - En la columna *Superhost* se han completado las posibles opciones (True, False) y se ha incluido el valor "unknown" para los espacios en blanco.
    - Se ha procedido de igual manera para las columnas *Host_identity_verified* e *Instant_bookable*-
    - Se ha dividido el valor de la columna "Bathrooms" entre 10, de acuerdo a la explicación inicial de la columna en la que, por ejemplo, el valor 10 indica 1 baño y el valor 15 un baño y un aseo, es decir, 1,5 baños. Para mostrarlo, se ha creado la columna *Num. Bathrooms*.
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

Por otra parte, se han dejado casillas vacías en las columnas "Bedrooms", "Beds" y "Price_€" para el posterior análisis.

Tras esta limpieza y transformación de los datos, se crea un fichero csv con el que posteriormente se trabajará.


# 📊 Análisis Descriptivo Hosts
Para el análisis del perfil de los Hosts o Anfitriones de Airbnb, se eliminan las columnas relativas a los Listings o Anuncios publicados.

Del datasheet filtrado y transformado de fases anteriores que contaba con todos los datos, se ha hecho un paso de transformación más, eliminando los *Host_ID* duplicados. Es decir, para el análisis del perfil de Hosts en Madrid se cuenta con un datasheet de 11 columnas y 7.896 filas.

## 🔢 Análisis de las variables numéricas
### **Host_response_rate_num**
Para el análisis de esta variable se ha de tener en cuenta que de los datos originales vienen muchas casillas en blanco, por lo que para el análisis de las variables estadísticas será necesario filtrarlas.

El total de valores en blanco de esta columna es igual a **903** que corresponde a un **11%** de los datos totales. Los **6.993 valores** restantes serán analizados:

- Media: 0,917 | Mediana: 1 | Moda: 1
- Mínimo: 0 | Máximo: 1 | Desviación estándar: 0,23
- Asimetría: -3,13 | Curtosis: 8,73

La media indica que en promedio los hosts responde al 91,7% de las consultas.

La mediana y la moda son ambas 1, lo que indica que más de la mitad son hosts que responden al 100% de los mensajes (además de ser el valor más frecuente).

La desviación estándar indica una variabilidad moderada. La curtosis indica una distribución leptocúrtica con muchos valores concentrados alrededor del 1y algunos casos extremos (ouliters). El coeficiente de asimetría, fuertemente negativo, indica que existe una cola hacia la izquierda, es decir, la mayoría de hosts tienen tasas de respuesta cercanas a 1 y hay unos pocos hosts con tasas muy bajas.

Como conclusión, se puede afirmar que los anfitriones (o hosts) en Madrid son muy diligentes respondiendo, de acuerdo a la altísima tasa de respueta. La asimetría negativa y la curtosis elevada confirman una distribución fuertemente concentrada en el valor máximo.


### **Host_acceptance_rate_num**
- Media: 0,813 | Mediana: 0,97 | Moda: 1
- Mínimo: 0 | Máximo: 1 | Desviación estándar: 0,30
- Asimetría: -1,73 | Curtosis: 1,73

En promedio, la tasa de aceptación de las solicitudes es del 81,3%.

De acuerdo a la mediana, el 50% de los anfitriones acepta al menos el 97% de las solicitudes y el valor más común es 100% (moda), la mayoría de anfitriones aceptan todas las solicitudes.

En este caso, la desviación existe pero no es extrema. El valor de la asimetría indica una distribución sesgada a la izquierda (la mayoría de valores están cerca del 1 - o del 100%), es decir, hay pocos anfitriones con tasas bajas. La curtosis muestra una distribución platicúrtica, es decir, leve concentración alrededor de la media sin valores extremos muy marcados.

Aunque son minoría (6,4%), existen anfitriones que no han aceptado ninguna solicitud (indicado por el valor mínimo 0). Esto puede significar que está inactivos o tienen los anuncios en mal estado.

En general, se observa una tendendia a mantener alta disponibiliad de respuesta por parte de los hosts para mejor la visibilidad de sus anuncios y reforzar la reputación en la plataforma.

### **Host_listings_count**
- Media: 5,28 | Mediana: 1 | Moda: 1
- Máximo: 3.311 | Desviación estándar: 52,55
- Asimetría: 41,77 | Curtosis: 2.232,58

De acuerdo a los datos estadísticos, en promedio cada host tiene unos 5 listings (anuncios). Sin embargo, este valor se ve distorsionado por los valores extremos existentes (outliers), pues el rango de valores es de 1 a 3311.

A través de la mediana y la moda se aprecia como la mitad de los host solo tiene un listing, siendo también el valor más repetido.

La distribución de la muestra es leptocúrtica: hay muchos valores cerca de la media pero altísimos valores extremos. La asimetría es positiva, hay muchos valores bajos (en concordancia con la mediana y la moda) y pocos valores muy altos. Esto, junto con la extrema asimetría (41,77) confirma que hay pocos valores que alejan la distribución de la normalidad.

### **Host_total_listings_count**
- Media: 7,85 | Mediana: 2 | Moda: 1
- Máximo: 8.554 | Desviación estándar: 113,17
- Asimetría: 59,68 | Curtosis: 4.230,17

Este valor indica el total de *listings* (o anuncios) de un *host* (anfitrión) en el momento de scrape en toda la página de Aribnb.

El promedio de los hosts que tienen anuncios en Madrid, tiene en total unos 8 anuncios. Sin embargo, como para el resto de variables, no es un valor representativo, pues la mediana indica un valor de 2 y la moda de 1. Es decir, la mitad de los anfitriones tiene 2 o menos anuncios, siendo 1 el valor más común.  Con esto, se puede afirmar que Airbnb tiene un fuerte componente de hosts particulares.

La desviación estándar indica que, en este caso, sí hay valores muy alejados del promedio. La curtosis leptocúrtica y extrema refuerza esta afirmación: muchos valores bajos y unos pocos outliers enormes, lo que indica una distribución extremadamente sesgada a la derecha (asimetría positiva).


## 📈 Análisis de las variables categóricas
### Host_location
Esta variable indica el país de procedencia del host. Cabe destacar que el 33,5% de los hosts han preferido no indicar su procedencia, por lo que han sido clasificados como "unknown".

Del resto de datos disponible se destaca lo siguiente: 
- España concentra el 75% de los hosts, con 5.254 registros.
- Existe mucha diferencia con los siguientes países más representados: Estados Unidos (0,8%), Reino Unido (0,6%), Francia (0,34%) y México (0,26%).

En el mapa siguiente se puede ver la distribución de la procedencia de los Hosts:

![Mapa de localización de los Hosts](Images\Hosts_map.png)

### Host_response_time
Esta variable está relacionada con la anterior variable numérica *Host_response_time_num*, ilustrando la misma información agrupada según el tiempo de respuesta de cada host.

![](Images\Host_response_time.png)

En el gráfico superior se observa como el 62,5% de los hosts responde dentro de una hora, lo que indica un alto nivel de inmediatez. 

Agrupando los hosts que responden en pocas horas (13,4%) y los que responde dentro del mismo día (6,9%), el 82,8% de los hosts responde en menos de un día. Esto favorece el uso de Airbnb y mejor la confianza del cliente con respecto a los anfitriones. 

### Superhost

Del total de anfitriones analizados en la muestra para Madrid, tan solo el 33,68% está considerado superhost para Airbnb. Esto quiere decir que al menos 1 de cada 3 anfitriones cumple los requesitos específicos de Airbnb para alcanzar esta categoría, que son:
1. Tasa alta de respuesta: contestar al menos el 90% de los mensajes en 24 horas.
2. Tasa baja de cancelación: mantener las cancelaciones al mínimo (1% o menos).
3. Calificación excelente: tener una media de 4,8 estrellas en las evaluaciones.
4. Experiencia suficiente: al menos 10 estancias.

Esto les puede otorgar mayor visibilidad o mayor confianza por parte del cliente.

*Debido a la falta de información inicial para este proyecto con respecto a las variables necesarias para alcanzar el rango *Superhost* no se va a analizar en detalle la relación con las mismas.*

### Host_verification
Los anfitriones dentro de Airbnb tienen distintas posibilidad de contactar con los clientes y viceversa. 

![Medios de verificación](Images\Host_verification.png)

La combinación más común corresponde a las verificaciones por correo electrónico (email) y por teléfono (78,95%). Un 7,7% adicional añade la verificación mediante correo profesional, lo que puede indicar un nivel extra de profesionalidad o vinculación corporativa.

El 12,9% correspondiente a la verificación única por teléfono puede significar que son perfiles más antiguos o más básicos, pero no se dispone información suficiente para verificarlo.

### Identity_verified
Esta variable indica si la identidad del anfitrión está enteramente verificada. 

Como se observa en el gráfico inferior, un 96,11% de los anfitriones están correctamente verificados por Airbnb, lo que indica alto nivel de confianza y seguridad para los huéspedes. 

![Verificación de identidad](Images\Identity_verification.png)


## 📅 Análisis temporal
### Host_since
Esta variable indica desde cuando el anfitrión pertenece a la plataforma de Airbnb. 

En la gráfica temporal se puede observar el crecimiento de uso y confianza depositado en la plataforma a lo largo de los años y cómo, en relación al turismo general, a la pandemia de 2019 y a distintos factores geopolíticos, ha ido evolucionando: 

![Host since](Images\Host_since.png)

------------------------------------------------------------------------------------
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


