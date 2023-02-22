[//]: # (Portada)
# Instituto Tecnológico de Costa Rica

# Escuela de Computación

# Bases de Datos II GR 1

# Asigancion

# Titulo

# Estudiante: 
# Carlos Eduardo Leiva Medaglia / 2021032973

# Profesor: 
# Gerardo Nereo Campos Araya

# I Semestre 2023
[//]: # (Dejo esto para que el siguiente texto inicie en una nueva pagina)
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
[//]: # (Resumen pequeño sobre que es elastic search)
# Elastic Search  

Elasticsearch es un motor de búsqueda y de análisis el cual nos puede proporcionar estas herramientas casi en tiempo real para cualquier tipo de dato. De igual manera, Elasticsearch nos ofrece velocidad para el manejo de datos en distintos casos de uso, algunos ejemplos pueden ser:

* Automatiza flujos de trabajo usando Elasticsearch como un motor de almacenamiento
* Usa aprendizaje automático para modelar el comportamiento de datos.
* Analiza y procesa datos genéticos
* Almacena y analiza datos de eventos de seguridad.  

Como se puede ver Elasticsearch puede ser utilizado para gran variedad de usos y también es una gran herramienta para utilizar en la solución de nuestros problemas.

[//]: # (Resumen de la primera seccion del documento)

## Documentos e Indices
Elasticsearch almacena documentos como estructura de datos que han sido serializadas en documentos JSON. Cuando un documento esta almacenado se puede realizar la búsqueda de este en tiempo real.  
Un índice es una colección optimizada de documentos, y su vez, estos documentos son una colección de campos, estos campos son pares "clave-valor" donde contiene los datos. Cada campo indexado va a tener su propia estructura de datos optimizada, por ejemplo, los campos de texto se almacenan en índices invertidos, esto lo que hace es enumerar cada palabra única que aparece en un documento y luego reconoce todos los documentos donde aparece la palabra. Es importante recordar que un documento puede tener distintos campos, los cuales pueden ser manejados de distintas maneras, como lo fue mencionado con los campos de texto.  
Sin embargo, Elasticsearch nos da la posibilidad de poder indexar sin especificar como se va a manejar cada campo que puede aparecer en un documento. La manera en que funciona esto es con el mapeo dinámico, lo que pasara es que se agregaran automáticamente nuevos campos al índice, esto permite comenzar a indexar documentos y a su vez detectara y asignar valores a los tipos de datos correspondientes, gracias a esto podremos indexar y explorar datos.
Es importante mencionar, que se pueden definir reglas propias para el mapeo dinámico. Esto puede traernos ventajas, una por ejemplo seria, usar formatos de fecha personalizados.  
Por último, a veces, es conveniente indexar el mismo campo de diferentes maneras, realizando esto se nos amplia la manera en la que podríamos obtener resultados de la indexación de un campo especifico.

[//]: # (Resumen de la segunda seccion del documento)

## Busqueda y Analisis
### Busqueda
Elasticsearch tiene un gran poder en lo que son sus capacidades de búsqueda, estas están construidas en la librería de Apache Lucene, gracias a esto se puede realizar búsquedas y análisis de datos muy sorprendente.
Para la búsqueda de datos admite distintos tipos de consulta que podemos realizar dependiendo en base a que necesitemos realizar la búsqueda.
Entre estos tipos de consulta se encuentra la consulta estructurada, que es un tipo de consulta al estilo SQL, ya que nos permite buscar por campos específicos. Otro tipo es la consulta de texto completo, la cual encuentra documentos que contengan coincidencias de una palabra o una frase especifica.
### Análisis
Elasticsearch utiliza las agregaciones, las cuales nos permiten realizar análisis de nuestros datos de una manera muy completa. Las agregaciones son igual de veloces que las búsquedas, por lo que podemos analizar nuestros datos en tiempo real, esto nos permite que conforme se actualizan nuestros datos, los análisis de estos también irán cambiando.

> **Importante mencionar que tanto las búsquedas y las agregaciones pueden trabajar juntas, lo que permite, realizar búsquedas, y a su vez, hacer análisis de los resultados de estas.**

[//]: # (Resumen de la segunda seccion del documento)

## Clusters, Nodos y Shards

Elasticsearch puede agregar nodos a los clústeres, automáticamente se distribuyen los datos y consultas en los nodos disponibles. Elasticsearch puede equilibrar automáticamente los clústeres para que funcionen de acuerdo a la cantidad de nodos que haya.
Elasticsearch cuenta con lo que son shards, y estos shards son índices. Cuando un documento se distribuye en un índice a través de un shard, y a su vez, este shard se distribuye en varios nodos, esto nos garantiza una protección contra fallas de hardware y aumentara la capacidad de consultas.
Existen dos tipos de shards: primarios y replicas. Un shard primario es cada documento en un índice, mientras que las réplicas, son copias de un shard primario. El número de shards primarios se fija al crear un índice, al contario de las réplicas las cuales su cantidad puede ser cambiada en el momento que se guste.
Existen algunas limitaciones que hay que tener en cuenta en cuanto al tamaño del shard. Cuando el tamaño es muy grande puede que se necesite más tiempo en caso de requilibrar un clúster. En caso de ser muy pequeño puede hacer el procesamiento más rápido, pero traería más consultas, por lo tanto, más sobrecarga. Se recomienda un rango entre 20GB y 40GB, sin embargo, se recomienda realizar prueba y error, y ver que funciona mejor en cada caso.
Existe un término llamado replicación entre clústeres, y como su nombre lo dice, es clonar varios clústeres, teniendo un clúster como principal. De esta manera en caso de que el clúster principal deje de funcionar, tendríamos un secundario que lo pueda respaldar.
Es importante mencionar que ElasticSearch permite utilizar Kibana como centro de control para administrar clústeres.








