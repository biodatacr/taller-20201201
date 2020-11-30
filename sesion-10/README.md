# Información y datos geográficos

La información y los datos geográficos (a veces llamados también espaciales o geoespaciales) hacen referencia a la localización de un objeto o fenómeno en un espacio geográfico. Esta referencia puede ser implícita (ej. mediante el nombre de un lugar) o explícita, en un [sistema de coordenadas](https://en.wikipedia.org/wiki/Geographic_coordinate_system).

## Tipos de datos

Hay dos tipos de datos geográficos: vectoriales y raster.

### Datos vectoriales
El modelo vectorial de datos está basado en puntos localizados en un sistema de coordenadas. Los puntos individuales pueden representar objetos independientes (ej. la localización de un poste eléctrico o de una cabina telefónica) o pueden también agruparse para formar geometrías más complejas como líneas o polígonos. Por lo general, los puntos tienen solo dos dimensiones (x, y), a las que se les puede agregar una tercera dimensión _z_, usualmente correspondiente a la altitud sobre el nivel del mar.

#### El estándar Simple Features
[Simple Features](https://www.ogc.org/standards/sfa) (o Simple Feature Access) es un estándar abierto de la [Organización Internacional de Estandarización (ISO)](https://iso.org/) y del [Open Geospatial Consortium (OGC)](https://www.ogc.org/) que especifica un modelo común de almacenamiento y acceso para geometrías de dos dimensiones (líneas, polígonos, multilíneas, multipolígonos, etc.). El estándar es implementado por muchas bibliotecas y bases de datos geoespaciales como [sf](https://cran.r-project.org/web/packages/sf/index.html), [GDAL](https://gdal.org/), [PostgreSQL/PostGIS](https://en.wikipedia.org/wiki/PostGIS), [SQLite/SpatiaLite](https://www.gaia-gis.it/fossil/libspatialite/), [Oracle Spatial](https://www.oracle.com/database/technologies/spatialandgraph.html) y [Microsoft SQL Server](https://www.microsoft.com/en-us/sql-server/), entre muchas otras.

La especificación define 17 tipos de geometrías, de las cuales siete son las más comúnmente utilizadas. Estas últimas se muestran en la figura 1.

<figure>
  <img src="img/sf_types.png" alt="Tipos de geometrías de Simple Features más usadas">
  <figcaption><strong>Figura 1.</strong> Tipos de geometrías de Simple Features más usadas. Imagen de Robin Lovelace et al. (https://geocompr.robinlovelace.net/spatial-class.html#vector-data)</figcaption>
</figure>

### Datos raster
El modelo de datos raster usualmente consiste de un encabezado y de una matriz con celdas (también llamadas pixeles) de un mismo tamaño. El encabezado define el sistema de coordenadas, la extensión y el punto de origen de una capa raster. Por lo general, el origen se ubica en la esquina inferior izquierda o en la esquina superior izquierda de la matriz. La extensión se define mediante el número de filas, el número de columnas y el tamaño (resolución) de la celda.

Cada celda tiene una identificación (ID) y almacena un único valor, el cual puede ser numérico o categórico, como se muestra en la figura 2. 

<figure>
  <img src="img/modelo_raster.png" alt="El modelo raster: (A) ID de las celdas, (B) valores de las celdas, (C) mapa raster de colores">
  <figcaption><strong>Figura 2.</strong> El modelo raster: (A) ID de las celdas, (B) valores de las celdas, (C) mapa raster de colores. Imagen de Robin Lovelace et al. (https://geocompr.robinlovelace.net/spatial-class.html#raster-data)</figcaption>
</figure>
<p>

A diferencia del modelo vectorial, el modelo raster no necesita almacenar todas las coordenadas de cada geometría (i.e. las esquinas de las celdas), debido a que la ubicación de cada celda puede calcularse a partir de la información contenida en el encabezado. Esta simplicidad, en conjunto con el [álgebra de mapas](https://en.wikipedia.org/wiki/Map_algebra), permiten que el procesamiento de datos raster sea mucho más eficiente que el procesamiento de datos vectoriales. Por otra parte, el modelo vectorial es mucho más flexible en cuanto a las posibilidades de representación de geometrías y almacenamiento de valores, por medio de múltiples elementos de datos.

Los mapas raster generalmente almacenan fenómenos continuos como elevación, precipitación, temperatura, densidad de población y datos espectrales. También es posible representar mediante raster datos discretos, tales como tipos de suelo o clases de cobertura de la tierra, como se muestra en la figura que se muestra en la figura 3.

<figure>
  <img src="img/raster_continuo_categorico.png" alt="Ejemplos de mapas raster continuos y categóricos">
  <figcaption><strong>Figura 3.</strong> Ejemplos de mapas raster continuos y categóricos. Imagen de Robin Lovelace et al. (https://geocompr.robinlovelace.net/spatial-class.html#raster-data)</figcaption>
</figure>

## Software
El software para manejo de datos e información geoespaciales incluye diversos tipos de aplicaciones, incluyendo servidores (ej. [GeoServer](http://geoserver.org/), [MapServer](https://mapserver.org/)), motores de bases de datos (ej. [PostgreSQL/PostGIS](https://postgis.net/), [Oracle Spatial](https://www.oracle.com/database/technologies/spatialandgraph/spatial-features.html)) y programas de escritorio (ej. [QGIS](https://www.qgis.org/), [ArcGIS Dektop](https://desktop.arcgis.com/)), entre otros.

Todo este software está basado en varias bibliotecas que realizan funciones fundamentales, como conversiones entre formatos, operaciones geométricas y reproyecciones cartográficas. Entre las principales de estas bibliotecas pueden mencionarse:

* **GDAL**: [Geospatial Data Abstraction Library (GDAL)](https://gdal.org/) es una biblioteca para leer y escribir datos geoespaciales en varios formatos [raster](https://gdal.org/drivers/raster/) y [vectoriales](https://gdal.org/drivers/vector/). Implementa un único [modelo abstracto de datos raster](https://gdal.org/user/raster_data_model.html) y un único [modelo abstracto de datos vectoriales](https://gdal.org/user/vector_data_model.html), lo que permite programar aplicaciones geoespaciales sin tener que ocuparse de las particularidades de cada formato que se utilice (GeoTIFF, NetCDF, ESRI Shapefile, GeoJSON, etc.). A pesar de que GDAL está programada en C/C++, cuenta con una interfaz de programación de aplicaciones (API) para varios lenguajes de programación, incluyendo [C](https://gdal.org/api/index.html#c-api), [C++](https://gdal.org/api/index.html#id3), [Python](https://gdal.org/python/index.html) y [Java](https://gdal.org/java/overview-summary.html). Además, ofrece un conjunto de [utilitarios de línea de comandos](https://gdal.org/programs/) cuyas [distribuciones binarias](https://gdal.org/download.html#binaries) están disponibles para varios sistemas operativos, incluyendo Windows, macOS y Linux.
* **GEOS**: [Geometry Engine, Open Source (GEOS)](https://trac.osgeo.org/geos) es una implmentación en C++ de la biblioteca [JTS Topology Suite](http://www.tsusiatsoftware.net/jts/main.html) (desarrollada en Java) y que implementa un conjunto de operaciones y predicados geoespaciales (ej. unión, intersección, distancia, área).
* **PROJ**: [PROJ](https://proj.org/) es una biblioteca que transforma coordenadas entre diferentes CRS, incluyendo tanto proyecciones cartográficas como transformaciones geodésicas.

## Ejemplos de manejo de datos geográficos
### Utilitatios de línea de comandos de GDAL
La bilbioteca GDAL cuenta con un conjunto de [utilitarios de línea de comandos](https://gdal.org/programs/) cuyas [distribuciones binarias](https://gdal.org/download.html#binaries) están disponibles para varios sistemas operativos, incluyendo Windows, macOS y Linux. También están incluídos en la plataforma de ciencia de datos llamada [Anaconda](https://www.anaconda.com/), la cual cuenta con versiones para todos los sistemas operativos mencionados. Para el caso de Windows, están disponibles a través de [OSGeo4W](https://www.osgeo.org/projects/osgeo4w/), un conjunto de aplicaciones geoespaciales que puede instalarse junto con QGIS, entre otras opciones.

#### Ejemplos de comandos
**Listado de las capas disponibles en el [servicio WFS de cartografía 1:5000 del Instituto Geográfico Nacional (IGN)](https://www.snitcr.go.cr/ico_servicios_ogc_info?k=bm9kbzo6MjY=&nombre=IGN%20Cartograf%C3%ADa%201:5mil) en el [Sistema Nacional de Información Territorial (SNIT)](https://www.snitcr.go.cr/)**
```shell
$ ogrinfo WFS:"http://geos.snitcr.go.cr/be/IGN_5/wfs"
```
```
INFO: Open of `WFS:http://geos.snitcr.go.cr/be/IGN_5/wfs'
      using driver `WFS' successful.
Metadata:
  ABSTRACT=This is the reference implementation of WFS 1.0.0 and WFS 1.1.0, supports all WFS operations including Transaction.
  PROVIDER_NAME=The Ancient Geographers
  TITLE=SNIT Web Feature Service
1: IGN_5:forestal2017_5k
2: IGN_5:indice_5000
3: IGN_5:cultivos2017_5k
4: IGN_5:curvas_5000
5: IGN_5:delimitacion2017_5k
6: IGN_5:edificaciones2017_5k
7: IGN_5:hidrografia_5000
8: IGN_5:limitecantonal_5k
9: IGN_5:limitedistrital_5k
10: IGN_5:limiteprovincial_5k
11: IGN_5:linea_costa_5000
12: IGN_5:pastos2017_5k
13: IGN_5:urbano_5000
14: IGN_5:vias_5000
```

**Descarga de la capa de provincias**
```shell
# Descarga en formato GeoJSON, proyección WGS84 y con validación de geometrías
ogr2ogr -f GeoJSON -t_srs EPSG:4326 -makevalid provincias.geojson WFS:"http://geos.snitcr.go.cr/be/IGN_5/wfs" "IGN_5:limiteprovincial_5k"
```

