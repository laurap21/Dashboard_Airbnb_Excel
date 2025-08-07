# 🏡 Análisis de Datos Abiertos de Airbnb en Madrid
Curso: Data Analytics V3 | Proyecto: Dashboard &amp; Análisis de Datos

Este proyecto tiene como objetivo analizar los datos abiertos de Airbnb en la ciudad de Madrid. A lo largo del proyecto se realiza una transformación y limpieza de datos, análisis descriptivo, creación de un dashboard interactivo y elaboración de un informe explicativo con las principales conclusiones.

El informe inicial con el problema de análisis planteado es el siguiente: [Informe Inicial](Informe_inicial.md) y el README: [README](README.md).

El objetivo principal tras el análisis es crear un dashboard visual de los perfiles de los *hosts* (anfitriones) y de los *listings* (anuncios) para entender la situación de la oferta actual en Madrid.


## ⚙️ DESARROLLO DEL PROYECTO

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


# 👩🏼‍💼 Análisis Descriptivo Hosts
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

![Mapa de localización de los Hosts](/Images/Hosts_map.png)

### Host_response_time
Esta variable está relacionada con la anterior variable numérica *Host_response_time_num*, ilustrando la misma información agrupada según el tiempo de respuesta de cada host.

![](/Images/Host_response_time2.png)

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

![Medios de verificación](/Images/Host_verification2.png)

La combinación más común corresponde a las verificaciones por correo electrónico (email) y por teléfono (78,95%). Un 7,7% adicional añade la verificación mediante correo profesional, lo que puede indicar un nivel extra de profesionalidad o vinculación corporativa.

El 12,9% correspondiente a la verificación única por teléfono puede significar que son perfiles más antiguos o más básicos, pero no se dispone información suficiente para verificarlo.

### Identity_verified
Esta variable indica si la identidad del anfitrión está enteramente verificada. 

Como se observa en el gráfico inferior, un 96,11% de los anfitriones están correctamente verificados por Airbnb, lo que indica alto nivel de confianza y seguridad para los huéspedes. 

![Verificación de identidad](/Images/Identity_verification2.png)


## 📅 Análisis temporal
### Host_since
Esta variable indica desde cuando el anfitrión pertenece a la plataforma de Airbnb. 

En la gráfica temporal se puede observar el crecimiento de uso y confianza depositado en la plataforma a lo largo de los años y cómo, en relación al turismo general, a la pandemia de 2019 y a distintos factores geopolíticos, ha ido evolucionando: 

![Host since](/Images/Host_since2.png)

## 🗂️ Análisis bivariable
Para entender la posible relación entre las distintas variables, se ha hecho un análisis de correlación. Previo a esto, ha sido necesario asignar a ciertas variables categóricas un valor numérico siguiendo un criterio lógico. Las variables a las que se les ha asignado un valor son las siguientes: *Host_response_time*, *Superhost* y *Host_identity_verified*. Esto se ha hecho de la siguiente forma: 
- Para la categoría *Host_response_time* se han considerado los valores estipulados en la siguiente tabla:

    | Nombre inicial      | Valor asignado  |
    |---------------------|-----------------|
    | N/A                 | 0               |
    | whithin an hour     | 4               |
    | whithin a few hours | 3               |
    | a few fays or more  | 2               |
    | whithin a day       | 1               |

- De igual manera, para las variables *Superhost* y *Host_identity_verified* se han asignado valores de la siguiente forma:

    | Nombre inicial      | Valor asignado  |
    |---------------------|-----------------|
    | False               | 1               |
    | Unknown             | 0               |
    | True                | 2               |


La matriz resultante es la siguiente: 
![Matriz Correlaciones](/Images/Matriz_correlaciones_Hosts.png)

Se puede observar que no existe gran correlación entre estas variables salvo, cómo es lógico, las variables *Host_response_time* y *Host_response_rate_num* ya que hablan de lo mismo. De igual manera, se ve que las variables que hacen referencia al ratio de tiempo de respuesta y de aceptación tienen una correlación elevada. Los Hosts con mayor ratio de aceptación son los que menor tiempo de respuesta tienen (es decir, los que mayor porcentaje de respuesta tienen).

De igual manera, se observa una correlación positiva muy cerana al 1 en las variables *Hos_listing_count* y *Host_total_listings_count*, lo que indica que los *hosts* o anfitriones con más anuncios (o *listings*) en Madrid son también los que más anuncios tienen en toda la web de Airbnb. Esto quiere decir que existe una alta probabilidad de que sean usurarios profesionales en lugar de particulares.  

# 🛏️ Análisis Descriptivo Listings
Para el análisis del perfil de los Listings o Anuncios de Airbnb, se eliminan las columnas relativas a los Hosts o Anfitriones.

Del datasheet filtrado y transformado de fases anteriores que contaba con todos los datos, se ha hecho un paso de transformación más, extrayendo únicamente el año para las *reviews*, tanto para la primera (*First_review*) como para la última (*Last_review*). Es decir, para el análisis de los Litings tipo en Madrid se cuenta con un datasheet de 23 columnas y 19.275 filas.

## 🔢 Análisis de las variables numéricas
### Num. Accommodates
- Media: 3,3 | Mediana: 3 | Moda: 2
- Mínimo: 1 | Máximo: 16 | Desviación estándar: 1,93
- Asimetría: 1,65 | Curtosis: 5,24

Según el análisis estadístico, en promedio los alojamientos hospedan unas 3-4 personas. El error típico es muy bajo, lo que indica precisión en el cálculo de esta media. 
La mitad de los alojamientos alojan hasta 3 personas, aunque la capacidad de hospedaje más frecuente es de 2 personas. Todo esto sugiere que el mercado está principalmente orientado a parejas o pocos viajeros.

Los alojamientos van desde capacidad para 1 persona hasta para grupos de 16 personas.  

La variabilidad de la muestra es moderdada, de acuerdo a la desviación estándar.

El coeficiente de asimetría positivo indica que la distribución está fuertemente sesgada a la derecha, es decir, hay pocos alojamientos con capacidades muy altas que elevan la media (outliers). En cuento a la curtosis, indica que la distribución es leptocúrtica,  (muchos alojamientos se concentran cerca de la moda o mediana, existiendo valores extremos como se mencionaba anteriormente).

En la imagen siguiente se puede apreciar la forma de la distribución: 
![Num. Accommodates](/Images/Num_Accommodates2.png)

### Num. Bathrooms
En el estudio de esta variable es importante destacar que los valores con decimales tipo X,5 indican la presencia de un asep (sin ducha ni bañera), mientras que los valores enteros representan baños completos.

- Media: 1,29 | Mediana: 1 | Moda: 1
- Mínimo: 0 | Máximo: 15 | Desviación estándar: 0,63
- Asimetría: 3,26 | Curtosis: 25,50

La media indica que los alojamientos disponene entre 1 y 2 baños/aseos. La mediana muestra que al menos el 50% de los alojamientos disponen de 1 solo baño o aseo y, de igual manera, la moda muestra que el valor más frecuentes es igualmente de 1. 

Dado que los valores decimales (X,5) representan aseos (en lugar de baños completos), la media de 1,29 refleja que, además del baño principal, algunos alojamientos disponen de un aseo adicional, aumentando levemente el promedio respecto a la mediana y a la moda.

El valor de la desviación estandar señala que hay poca variablidad en el número de baños, concentrándose fuertemente alrededor del valor modal (1). El amplio valor del rango (de 1 a 15) indica la presencia de casos extraordinarios con un número muy elevado de baños, probablemente correspondiendo a grandes viviendas, edificios segmentados o alojamientos con baños compartidos.

La asimetría de esta distribución es positiva, con una larga cola a la derecha debido a la presencia de unos pocos alojamientos con muchos baños. La curtosis indica una distribución extremadamente leptocúrtica: la mayoría de alojamientos se agrupan muy fuertemente alrededor del valor central. De nuevo, esto indica que hay valores extremos.

![Num. Bathrooms](/Images/Num_Bathrooms2.png)

### Bedrooms
- Media: 1,38 | Mediana: 1 | Moda: 1
- Mínimo: 0 | Máximo: 25 | Desviación estándar: 0,94
- Asimetría: 3,44 | Curtosis: 43,06

En promedio, los alojamientos de la muestra cuentan con 1-2 dormitorios. El valor de la mediana y la moda coinciden en 1, evidenciando que el número de dormitorios más común y el punto central de la distribución son el mismo. La desviación de la media frente a estos valores indica que hay algunos alojamientos con más habitaciones, lo que eleva la media. 

La desviación estándar muestra una variabilidad moderada, la mayoría de alojamientos se encuentran cerca del valor modal, aunque existe cierta dispersión. El rango de 0 a 25 dormitorios indica que existen alojamientos que pueden ser un estudio (sin habitaciones) o que existen casos, como villas, fincas o alojamientos compartidos, que tienen un elevado número de dormitorios y distorsionan el rango.

El coeficiente de asimetría indica que ésta es positiva, con una cola larga hacia la derecha. Esto concuerda con la presencia de outliers o pocos alojamientos con muchas habitaciones. De igual manera, la distribución extremadamente leptocúrtica, confirma la concentración alrededor del valor central junto a una mayor frecuencia de valores atípicos.

![Bedrooms](/Images/Bedrooms2.png)

### Beds
- Media: 1,98 | Mediana: 2 | Moda: 1
- Mínimo: 0 | Máximo: 40 | Desviación estándar: 1,46
- Asimetría: 3,92 | Curtosis: 44,96

La media indica que, en promedio, los alojamientos tienen aproximadamente 2 camas, lo que resulta coherente con un mercado orientado a pequeños grupos o parejas. En este caso, mediana y moda no coinciden. La mediana (2) señala que al menos el 50% de los alojamientos disponen de 2 camas o menos, mientras que la moda (1) indica que el número más frecuente de camas es 1. 

Un rango elevado, de 0 a 40 camas, revela la existencia de propiedades excepcionales, probablemente grandes propieddades para grupos o con camas/habitaciones compartidas. La desviación estándar muestra una dispersión mayor que en las variables anteriormente analizadas, lo que sugiere mayor variedad en la configuración de camas. 

El coeficiente de asimetría altamente positivo indica que la mayoría de alojamientos tienen pocas camas aunque existen algunos con un elevado número de camas. La curtosis, extremadamente leptocúrtica, evidencia que los datos están fuertemente concentrados alrededor de los valores bajos, pero con colas largas que reflejan la presencia de numerosos vazlores atípicos.

![Beds](/Images/Beds2.png)

### Price_€
- Media: 138,89€ | Mediana: 97€ | Moda: 80€
- Mínimo: 8€ | Máximo: 23.124€ | Desviación estándar: 433,61€
- Asimetría: 31,29 | Curtosis: 1.248,21

La media indica el precio promedio por noche de la muestra, que en este caso no es representativo dada la gran variabilidad. La mediana, significativamente menos a la media revela una distribución que no es simétrica y confirma que la mayoría de los precios tienen precios por debajo del promedio. La moda, el precio más frecuente, muestra el punto de máxima concentración. Es decir, a pesar de que el promedio está alrededor de 139€, la mayoría de los alojamientos se sitúan más cerca de 80-100€.

La alta desviación estándar indica la gran variabilidad de los precios, también reflejada en el gran rango de valores (8 - 23.124€). Esto se puede deber a la existencia de propiedades muy exclusivas o valores erroneos/atípicos. Al no conocer el origen de datos y no poder comprobar si son correctos o no, se han considerado válidos pero extremadamente atípicos. Se debería realizar un análisis en profundidad de esto.

La asimetría, de nuevo altamente positiva, indica que la gran mayoría de precios son bajos o moderados pero existen unos pocos alojamientos lujosos con precios muy elevados (o atípicos, como se comenta en el párrafo anterior). De igual manera, la curtosis letpocúrtica, evidencia la presencia de valores extremos.

![Price](/Images/Price2.png)

### Minimum_nights
Esta variable está doblemente analizada, a nivel numérico y a nivel categórico, ya que se ha clasificado en niveles de exigencia según el número de noches (explicado anteriormente).

- Media: 7,74 | Mediana: 2 | Moda: 1
- Mínimo: 1 | Máximo: 700 | Desviación estándar: 20,07
- Asimetría: 9,00 | Curtosis: 151,41

La media de 7,74 indica que en promedio se exige un mínimo de 7-8 noches de reserva como mínimo. Sin embargo, la mediana evidencia que al menos la mitad de los alojamientos aceptan reservas muy cortas (de 2 noches o menos). El valor más frecuente revela que la política dominante es aceptar estancias mínimas de una sola noche, faiclitando la flexibilidad para estancias cortas.

La desviación estándar refleja una variabilidad muy alta en los requisitos mínimos de estancia. El rango, de 1 a 700 noches, evidencia la existencia de propiedades con requisitos extraordinariamente altos. Como se mencionaba anteriormente, en la transformación de datos, los requisitos de noches mínimas mayores a 365 se consideran "anuncios bloqueados", al ser tan elevadas.

El coeficiente de asimetría positivo significa que la mayoría exige estancias cortas, confirmado por la curtosis leptocúrtica.

![Minimum_nights](/Images/Min_nights2.png)

### Maximum_nights
Esta variable está doblemente analizada, a nivel numérico y a nivel categórico, ya que se ha clasificado en niveles de exigencia según el número de noches (explicado anteriormente).

- Media: 512,05 | Mediana: 365 | Moda: 365
- Mínimo: 1 | Máximo: 1.825 | Desviación estándar: 397,51
- Asimetría: 0,64 | Curtosis: -1,07

De media, los alojamientos aceptan reservas de hasta 512 noches (1 año y 5 meses). Sin embargo, la mediana y la moda coinciden en 365 noches.

La desviación estándar indica una dispersión muy amplia, casi tan grande como la media, reflejando la existencia de políticas diversas que permiten desde estancias muy cortas hasta periodos prolongados. El elevado rango podría indica que existen propiedades con mucha flexibilidad a la hora de reservar por noches, probablemente orientadas a alquiler temporal extendido. Sin embargo, los anuncios con un máximo de noches igual a 365 se han tratado como si no tuvieran un límite práctico, dado que raramente un huésped reserva estancias tan largas.

El coeficiente de asimetría indica una ligera asimetría positiva, con una cola que se extiende hacia valores más altos, pero mucho menos pronunciada que en variables anteriores. La curtosis, en este caso platicúrtica, implica que los valores están más dispersos y hay menos concentración extrema en torno a la media, pese a existir el pico en 365.

![Max_nights](/Images/Max_nights2.png)

### Availability_365
Esta variable está doblemente analizada, a nivel numérico y a nivel categórico, ya que se ha clasificado en niveles de exigencia según el número de noches (explicado anteriormente).

- Media: 173,16 | Mediana: 179 | Moda: 0
- Mínimo: 0 | Máximo: 365 | Desviación estándar: 126,62
- Asimetría: -0,01 | Curtosis: -1,47

La media de 173 días indica que en promedio los alojamientos están disponibles poco menos de la mitad del año. La mediana, similar a la media, indica que la mitad de los alojamientos tienen disponibilidad superior a 179 días del año. Por otro lado, en este caso la moda es igual a 0, que muestra que el valor más frecuente es que el alojamiento no esté disponible en ningún día del año. Esto podría deberse a anuncios inactivos, bloqueos temporales en el momento del scraping o propiedades ocupadas permanentemente.

La desviación estándar, bastante alta, muestra una gran diversidad en la disponibilidad: algunos alojamientos están prácticamente siempre disponibles mientras que otros no lo están casi nunca. El rango de 365 cubre completamente el año, mostrando la heterogeneidad de políticas o situaciones de los hosts.

El coeficiente de asimetría es prácticamente 0, lo que indica una distribución simétrica, sin sesgo claro hacia mayor o menor disponibilidad. La curtosis indica una distribución platicúrtica, con menos datos concentrados cerca del promedio. Esto sugiere que la disponibilidad se dispersa de forma más uniforme entre los diferentes valores, sin aglomerarse en torno a un único rango.

![Availability](/Images/Availability2.png)

### Number_of_reviews

- Media: 55,74 | Mediana: 16 | Moda: 0
- Mínimo: 0 | Máximo: 1.080 | Desviación estándar: 96,13
- Asimetría: 3,25 | Curtosis: 14,49

La media indica que en promedio los anuncios han recibidio alrededor de 55-56 opinones. La medaiana, de 16 reseñas, muestra que la mitad de los alojamientos tienen 16 o menos reseñas, mucho menor que la media. Esto refleja la influencia de algunos anuncios con altísimos números de reseñas. La moda vuelve a ser igual a 0, lo que indica que muchos alojamientos no tienen reseñas todavía (anuncios nuevos o con baja demanda).

La desviación estándar es muy alta en comparación con la media, evidenciando una dispersión considerable en el número de reseñas entre anuncios. Esto queda respaldado por el amplio rango de valores.

El coeficiente de asumetría indica una distribución altamente asimétrica positiva. La mayoría de anuncios tiene pocas reseña y solo una minoría concentra números muy elevados. La curtosis fuertemente leptocúrtica confirma que hay mucha concentración en casos con pocas reseñas, pero también existen valores extremos con cientos o miles de opiniones.

![Num. of reviews](/Images/Num_reviews.png)

## 📈 Análisis de las variables categóricas
### Neighbourhood_group_cleansed
Esta variable muestra en que distrito de la ciudad de Madrid se encuentra cada alojamiento. A continuación, el gráfico que lo representa:

![Neighbourhood](/Images/Neighbourhood.png)

El 43% de los alojamientos se encuentran ubicados en el distrito centro, desmarcándose del resto de ubicaciones, que oscilan entre un 0,3% y un 7%. Las zonas mejor comunicadas o más céntrica, como Tetúan o Salamanca, se corresponden con estos porcentajes cercanos a 7% mientras que cuánto más alejados o peor comunicados están, disminuye la oferta.

### Property_type y room_type
Para analizar el tipo de alojamiento o de estancia existen dos variables: 
- *Property_type* que indica cómo se ha caracterizado el alojamiento en la plataforma, y
- *Room_type* que hace referencia de forma más genérica al tipo de alojamiento o habitación en el que se hospedará el posible huésped.

Como se puede ver en el gráfico siguiente, existen muchos tipos de propiedades para clasificar un alojamiento, siendo el más común y estándar *Entire rental unit* que representa un 65% del total de la muestra. Esto puede deberse a que no es necesario especificar el tipo de propiedad tan específicamente, siendo que la mayoría serán apartamentos/pisos estándar. 

![Property_type](/Images/Property_type.png)

Por otro lado, para el usuario es más importante saber al tipo de estancia concreta en la que se va a hospedar, coincidiendo el valor más representativo anterior con el que se observa en el gráfico siguiente, *Entire home/apt.*, con un 72% del total.

![Room_type](/Images/Room_type.png)

### Shared_bathrooms
Otra variable caracterísitica de los alojamientos de alquiler es la posibilidad o no de tener baño privado. En la gráfica siguiente se observa que un 84% de los anuncios ofrecen baño privado en sus alojamientos, mientras que tan solo en un 16% de los mismos el baño sería compartido.

![Shared_bathrooms](/Images/Shared_bathrooms2.png)

### Minimum_night_category
Como comentado anteriormente, la variable numérica *Minimum_nights* se ha categorizado en distintas opciones en función de un rango de número de noches para así hacer más fácil el análisis y la comprensión del perfil de anuncios disponibles.

![Min_nights_cat](/Images/Min_nights_cat2.png)

Se puede apreciar como el mínimo de noches categorizado corresponde a *Very short stay* - estancias muy cortas - con un 75%, es decir, la mayoría de los anuncios no necesitan un mínimo de noches de reserva elevado.

### Maximum_nights_category
De igual manera que con la variable anterior, se han categorizado los valores de esta variable para mejorar la visibilidad de la muestra.

![Max_night_cat](/Images/Max_nights_cat2.png)

En este caso, y como se ha mencionado anteriormente, se ha considerado que los valores por encima de 365 implican que no hay límite significativo real en la reserva ya que podría ser considerado un alquiler estándar. Se aprecia, pues, que más de la mayoría de los alojamientos admite reservas largas, de hasta 1 año (55,33%) mientras que las reservas limitadas a estancias cortas o medias son escasas en comparación (7,34%).

### Annual_availability
Esta variable, también analizada previamente y categorizada para facilitar la comprensión, indica y refleja en el gráfico siguiente que a pesar de que el número más repetido de acuerdo con la moda sea 0, el rango de *high availability* abarca más valores (de 6 meses a un año).

Este gráfico muestra que el 47% de los alojamientos están disponibles al menos la mitad del años en la plataforma Airbnb, mientras que tan solo un 2,53% están siempre disponibles. Esto refleja que es poco común mantener la disponibilidad continua.

La categoría *Low availability* puede reflejar como el 26% de los alojamientos solo están disponibles hasta 3 meses al año, lo que puede estar relacionado con periodos vacacionales, por ejemplo.

![Availability_cat](/Images/Availability_cat2.png)

### Instant_bookable
Esta categoría muestra la facilidad o no de reservar automáticamente un alojamiento, sin pasar por la aprobación del *host* o anfitrión. 

En este caso los porcentajes son muy similares, siendo ligeramente mayor el número de alojamientos que necesitan la aprocación específica de su anfitrión. 

![Instant_bookable](/Images/Instant_bookable2.png)

## 🗂️ Análisis bivariable
En la matriz de correlaciones de los anuncios (o *listings*) se observa que puede existir una posible correlación entre varias variables.

![Matriz correlaciones](/Images/Matriz_correlaciones_Listings2.png)

**Correlaciones fuertes**:
- Existe una alta correlación entre el tipo de habitación (*room_type*) y si el baño es compartido o no (*shared_bathrooms*). En la gráfica comparativa se puede observar como en los apartamentos completos (*entire home/apt*) el baño, lógicamente, siempre es privado, mientras que para para habitaciones compartidas, el baño siempre será compartido. También se puede observar como las habitaciones de hotel son el tipo de alojamiento menos ofrecido (como se vio en el análisis anterior) y que para las habitaciones privadas, los porcentaje correspondientes a baño privado y compartido son muy similares.

![Shared_Bathrooms vs Room_type](/Images/Shared_bathrooms_vs_room_type2.png)

- También existe una alta correlación entre el número de camas (*beds*) y el número de huéspedes (*Num. Accommodates*). Es algo lógico, ya que cuántas más camas, más personas pueden quedarse en el alojamiento.

- Otras dos variables altamente relacionadas son el número de dormitorios (*bedrooms*) y el número de huéspedes (*Num. Accommodates*). De igual manera, es algo lógico que cuántos más huéspedes quepan en un alojamiento, más habitaciones tenga.

**Correlaciones moderadas**:
- De acuerdo con la información que proporciona la matriz de correlaciones, el precio (*Price_€*) apenas se relaciona con otras variables. Las correlaciones más altas con el número de camas (*beds*), el número de baños (*Num. Bathrooms*) y el número de huéspedes (*Num. Accommodates*). Esto sugiere que el precio depende de múltiples factores no representados en esta matriz, como pueden ser ubicación, temporada, etc. 

- La disponibilidad del alojamiento tampoco está relacionada con ninguna variable, la máxima existente es con las máximas noches permitidas de reserva, pero es muy baja. Esto implica que la disponibilidad anual no depende de las características físicas del alojamientos. 

**Otras correlaciones**
Una vez analizadas todas las variables y de cara a la realización del dashboard, se ha decidido que la segmentación principal sea por barrio. En el gráfico siguiente se muestra el precio medio por barrios, evidenciando que los más caros son los mejores ubicados en cuanto a turismo y comodidad.

![Precio medio](/Images/Precio_medio_barrio2.png)

## 🏁 CONCLUSIONES
Una vez analizados los datos se puedes extraer las siguientes conclusiones.

Para el perfil de **Hosts**: 
- En el momento de extracción de la muestra de la web de datos abiertos de Airbnb existían un total de **7.896** hosts o anfitriones.
- Tan solo el 27% del total de anfitriones tiene el calificativo de *Superhost*, para lo que hay que cumplir una serie de requisitos de Airbnb. Sin embargo, el 94% está correctamente verificado por la plataforma. Esto puede deberse a la presencia de anfitriones nuevos que aún no han completado el proceso de verificación o a cambios en sus perfiles que de igual manera no han sido comprobados del todo.
- El **49,81%** de los mismos tienen **entre 1 y 5 listings o anuncios**, lo que implica que no es su actividad profesional principal. En cambio, un **21,45%** de los anfitriones tiene **más de 50 anuncios publicados** (aunque no necesariamente disponibles), lo que lleva a la conclusión de que pueden ser cuentas profesionales cuya fuente de ingresos principal sea la gestión de alojamientos en Airbnb.
- Para mejorar la experiencia del usuario, existen dos variables principales a analizar: los medios de verificación y comunicación y el tiempo de respuesta. el **75,69%** de los anfitriones responden y están verificados por **correo electrónico y teléfono**, siendo los medios más comunes empleados por la población. El **69%** de los anfitriones responde a las peticiones en **menos de una hora**. 
- Por último, la gran mayoría de anfitriones en Madrid procede de España, pero hay una gran varibilidad de lugares de procedencia de los anfitriones, destacando por detás de España, EEUU, Reino Unido, México y Francia.

Para el perfil de los **Listings**:
- Existe un total de 19.274 anuncios publicados.
- El precio medio es de 138,89€. Este precio varía de forma significativa según el distrito en el que se encuentra el alojamiento. Por ejemplo, para el distrito centro, el precio medio es de 150€ mientras que para Carabanchel es de 79€. La moda y la mediana, de 97€ y 80€ respectivamente, indican que aunque hay anuncios más caros, el precio más representativo ronda los 80-100€.
- El **43%** de los alojamientos se concentra en el **distrito Centro**, que se corresponde con la zona más turística de la ciudad de Madrid y corrobora el sentido lógico de los precio más elevados.
- La mayoría de alojamientos, un **73,93%**, son apartamentos enteros, con una disponibilidad anual elevada (**47,76%**). 
- Por lo general, los alojamientos tienen un solo baño (71,86%) privado (84,09%).
- Solo un 47% de los anuncios son de reserva automática. Esto implica que a los anfitriones les gusta saber y comprobar quién se va a hospedar en su alojamiento. 
- El perfil de alojamientos principalmente se enfoca en viajes de corta duración (74,85%), para grupos reducidos o parejas ya que el número de huéspedes se centra entre 1 y 5 en el 86,64% del total de anuncios y la mayoría ofrece un único baño.

## ➡️ PRÓXIMOS PASOS
Para terminar de comprender el perfil de los anuncios en la ciudad de Madrid los próximos pasos del análisis son:
- Análsis de los alojamientos por Distrito, considerando número de huéspedes, baños, precio y número de habitaciones. 
- Relación entre variables categóricas y precio.
- Revisión de los datos iniciales en relación a las reseñas, contacto con el orgien de los datos.
- Breve informe por distrito describiendo el análisis realizado.
