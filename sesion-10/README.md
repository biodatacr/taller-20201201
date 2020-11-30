# Información y datos geográficos

La información y los datos geográficos (a veces llamados también espaciales o geoespaciales) hacen referencia a la localización de un objeto o fenómeno en un espacio geográfico. Esta referencia puede ser implícita (ej. mediante el nombre de un lugar) o explícita, en un [sistema de coordenadas](https://en.wikipedia.org/wiki/Geographic_coordinate_system).

Hay dos tipos de datos geográficos: vectoriales y raster

## Datos vectoriales
El modelo vectorial de datos está basado en puntos localizados en un sistema de coordenadas. Los puntos individuales pueden representar objetos independientes (ej. la localización de un poste eléctrico o de una cabina telefónica) o pueden también agruparse para formar geometrías más complejas como líneas o polígonos. Por lo general, los puntos tienen solo dos dimensiones (x, y), a las que se les puede agregar una tercera dimensión _z_, usualmente correspondiente a la altitud sobre el nivel del mar.

### El estándar Simple Features
[Simple Features](https://www.ogc.org/standards/sfa) (o Simple Feature Access) es un estándar abierto de la [Organización Internacional de Estandarización (ISO)](https://iso.org/) y del [Open Geospatial Consortium (OGC)](https://www.ogc.org/) que especifica un modelo común de almacenamiento y acceso para geometrías de dos dimensiones (líneas, polígonos, multilíneas, multipolígonos, etc.). El estándar es implementado por muchas bibliotecas y bases de datos geoespaciales como [sf](https://cran.r-project.org/web/packages/sf/index.html), [GDAL](https://gdal.org/), [PostgreSQL/PostGIS](https://en.wikipedia.org/wiki/PostGIS), [SQLite/SpatiaLite](https://www.gaia-gis.it/fossil/libspatialite/), [Oracle Spatial](https://www.oracle.com/database/technologies/spatialandgraph.html) y [Microsoft SQL Server](https://www.microsoft.com/en-us/sql-server/), entre muchas otras.

La especificación define 17 tipos de geometrías, de las cuales siete son las más comúnmente utilizadas. Estas últimas se muestran en la siguiente figura:

<figure>
  <img src="img/sf_types.png" alt="Tipos de geometrías de Simple Features más usadas">
  <figcaption>Tipos de geometrías de Simple Features más usadas. Imagen de Robin Lovelace et al. (https://geocompr.robinlovelace.net/spatial-class.html#vector-data)</figcaption>
</figure>


## Datos raster
El modelo de datos raster usualmente consiste de un encabezado y de una matriz con celdas (también llamadas pixeles) de un mismo tamaño. El encabezado define el sistema de coordenadas, la extensión y el punto de origen de una capa raster. Por lo general, el origen se ubica en la esquina inferior izquierda o en la esquina superior izquierda de la matriz. La extensión se define mediante el número de filas, el número de columnas y el tamaño (resolución) de la celda.

Cada celda tiene una identificación (ID) y almacena un único valor, el cual puede ser numérico o categórico, como se muestra en la figura siguiente. 

<figure>
  <img src="img/modelo_raster.png" alt="El modelo raster: (A) ID de las celdas, (B) valores de las celdas, (C) mapa raster de colores">
  <figcaption>El modelo raster: (A) ID de las celdas, (B) valores de las celdas, (C) mapa raster de colores. Imagen de Robin Lovelace et al. (https://geocompr.robinlovelace.net/spatial-class.html#raster-data)</figcaption>
</figure>
/

A diferencia del modelo vectorial, el modelo raster no necesita almacenar todas las coordenadas de cada geometría (i.e. las esquinas de las celdas), debido a que la ubicación de cada celda puede calcularse a partir de la información contenida en el encabezado. Esta simplicidad, en conjunto con el [álgebra de mapas](https://en.wikipedia.org/wiki/Map_algebra), permiten que el procesamiento de datos raster sea mucho más eficiente que el procesamiento de datos vectoriales. Por otra parte, el modelo vectorial es mucho más flexible en cuanto a las posibilidades de representación de geometrías y almacenamiento de valores, por medio de múltiples elementos de datos.

Los mapas raster generalmente almacenan fenómenos continuos como elevación, precipitación, temperatura, densidad de población y datos espectrales. También es posible representar mediante raster datos discretos, tales como tipos de suelo o clases de cobertura de la tierra, como se muestra en la figura que se muestra a continuación.

<figure>
  <img src="img/raster_continuo_categorico.png" alt="Ejemplos de mapas raster continuos y categóricos">
  <figcaption>Ejemplos de mapas raster continuos y categóricos. Imagen de Robin Lovelace et al. (https://geocompr.robinlovelace.net/spatial-class.html#raster-data)</figcaption>
</figure>


## Bibliotecas 
