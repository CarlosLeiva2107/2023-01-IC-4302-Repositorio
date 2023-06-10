[//]: # (Portada)
# Instituto Tecnológico de Costa Rica

# Escuela de Computación

# Bases de Datos II GR 1

# Examen

# Estudiante: 
# Carlos Eduardo Leiva Medaglia / 2021032973

# Profesor: 
# Gerardo Nereo Campos Araya

# I Semestre 2023
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
[//]: # (Resolucion Examen)

# Pregunta 1

1. ¿Qué motor de base de datos utilizaría para implementar la navegación entre distintos elementos de información? ¿Es necesario que este motor de base de datos contenga todo el elemento de información o solo palabras clave que permitan establecer relaciones? Justifique su respuesta mediante la elaboración de un pequeño modelo de datos y las relaciones que establecería entre los diferentes elementos de información, lo más importante es garantizar una navegación y que permita descubrir relaciones. (20 pts)  

Como motor de base de datos utilizaría uno que estuviera basado en Grafos, para poder mantener las relaciones entre cada elemento de información, y de esta manera lograr ese estilo de búsqueda como Wikipedia. Consideraría que no es necesaria almacenar toda la información del elemento, creo que con almacenar simplemente palabras claves que nos permitan establecer las relaciones podría funcionar. Los nodos en la base de datos se encargarían de tener el libro, el articulo científico o sitio web y las relaciones serán por tema, autor, etc. Un ejemplo de como podría verse esto seria:  

![Imagen](https://imgur.com/kQCoc1h.png)  

2. ¿Qué motor de base de datos utilizaría para almacenar los elementos de información y garantizar full text search? Justifique su respuesta comentando: (20 pts) a. Capacidad del motor para implementar full text search. b. Particionamiento o sharding de datos. c. Representación de elementos de información en la base de datos (tablas, documentos, collections, etc.)  

El motor que utilizaría para almacenar los elementos seria MongoDB, ya que este motor tiene la capacidad para implementar full text search y de una manera sencilla y eficiente, que permite realizar la búsqueda de palabras en todos los elementos y encontrar coincidencias. También MongoDB permite hacer sharding y podemos distribuir nuestros datos a traves de diferentes servidores. Los elementos serian guardados como documentos dentro de colecciones de MongoDB, y estos tendrán toda la información completa del elemento. Considero MongoDB una buena opción para implementar esto y es sencillo de usar, mas que es una base con la que ya tengo previa experiencia y se que funciona bien con esto.  

3. Describa la forma en la cual combinaría los dos motores anteriores (navegación y full text search) para crear un sistema simple de búsqueda y navegación de información similar al que tiene el sitio Wikipedia donde se busca un elemento de información y nos podemos mover entre términos. (5 pts)  

El sistema funcionaria de manera que cuando un usuario realice una búsqueda, el full text search de MongoDB encontrara las coincidencias y retornara estos documentos en donde el usuario podrá verlos completamente ya que MongoDB si devuelve los documentos completos. Una vez el usuario acceda a un documento este podrá tener subrayadas las palabras claves con las cuales tiene relación con otros documentos, si alguna de esta palabras es seleccionada, se puede usar el motor de base de datos de grafos para ver la relación que existe, y asi poder acceder a otro documento. Como el motor de base de datos de grafos no cuenta con toda la información almacenada, volvemos a usar MongoDB, pero esta vez solo obteniendo el documento necesario para que se muestre completamente.  

4. ¿De qué forma garantizaría alta disponibilidad de las bases de datos? (5 pts)  

Para garantizar alta disponibilidad a los usuarios primeramente consideraría tener distribuidos varios nodos que permitan realizar acciones de solo lectura, para lograr consultas de lecturas rápidas y que de esta manera se distribuya la carga entre varios nodos. También ya que se esta usando un Cloud Provider seria buena idea tener replicas geográficas, para evitar inconvenientes con los usuarios alrededor del mundo.  

5. ¿Cómo podría garantizar que las búsquedas siempre tengan un tiempo de respuesta constante (5pts)  

Para garantizar consistencia en las búsquedas esta la ventaja de que se implemento varios nodos de solo lecturas, esto hará que la carga de la consultas de lecturas se distribuyan y nos devuelva los resultados mucho mas rápido. Adicional a esto, se pueden implementar indices donde nuestra base de datos asi mejor lo requiera, dependiendo de las consultas y las frecuencias de estas es que se puede determinar en donde se puede implementar indices y asi agilizar la respuesta de estas.  

6. ¿Cómo el uso de caches y localidad podría mejorar el rendimiento del sistema? (5 pts)  

Principalmente el uso de caches ayudaría a mejorar el rendimiento del sistema, ya que en este podría estar almacenada información sobre consultas frecuentes, las cuales cuando estas sean ejecutadas se podrá acceder mucho mas rápido a la información ya que se encuentra en el cache, lo que nos proporcionaría mejores tiempos de respuesta. La localidad nos permitiría que los datos que se relacionan entre si sean mas fáciles de ser accedidos, por lo que si un usuario realiza una búsqueda, el resultado tendrá cerca también todo lo demás con lo que se relaciona.

# Pregunta 2  

- ¿Qué índices definiría para aumentar la velocidad de todo el sistema? Tome en cuenta todos los tipos de índices estudiados en el curso. (3 pts)  

Principalmente creo que definiría algunos expression index basados en las consultas mas usuales y de esta manera lograr mejorar el rendimiento de estas consultas. También crearía un partial index en las tablas de "artist" y "album" las cuales son tablas que son utilizadas bastante. También creo que podría ser buena idea agregar un non-clustered index en las distintas columnas que mas son utilizadas, y ya que se menciona que el sistema tiene altas lecturas bajas escrituras, no habrá problema, ya que con un non-clustered index aumentamos las lecturas pero esto puede hacer que duren las escrituras.  

- ¿Qué base de datos SQL o NoSQL recomendaría para reemplazar la base de datos actual? Justifique su respuesta. (3 pts).  

Como base de datos recomendaría utilizar Elasticsearch, ya que es una base de datos que permite realizar búsquedas rápidas en grandes cantidades de datos, y suponiendo que tenemos información almacenada sobre música, deben haber gran cantidad de datos los cuales deben responder a búsquedas de manera eficiente y rápida. Asi como también cuenta con un sistema distribuido en donde las cargas de trabajo se reparten entre si, lo que puede mejorar los tiempos de respuesta. Por lo anterior considero que Elasticsearch seria una buena opción de remplazo.  

- ¿Existirá alguna otra forma de mejorar el rendimiento de la base de datos relacional en especial para la tercera consulta? Comente. (4 pts)  

Para lograr mejorar el rendimiento en la base de datos relacional, lo que se puede hacer, como ya se menciono previamente es definir indices para que estos ayuden al rendimiento de las consultas. Asi como también aprovechar el uso de la cache para asi almacenar resultados de las consultas usuales y obtener un mejor tiempo de respuesta. Inclusive si se desea seguir con la base de datos relacional se puede realizar un análisis de su diagrama para asi encontrar fallos que puedan estar generando posible retrasos o también se puede analizar la forma en la que se están planteando la consulta, ya que tal vez no esta de la forma mas optima y se pueda encontrar una forma mas eficiente de realizar esta.  

# Pregunta 3  

Basado en el diagrama anterior para cada componente hay formas en las que se puede aplicar la seguridad para evitar tener problemas.  

- En la aplicación se deben implementar buenas practicas de programación para evitar problemas de seguridad, como lo puede ser revisar todas las entradas de datos posibles para asi evitar inyecciones de código. Fundamental que no se utilice ninguna contraseña o información de valor dentro del código de esta.  
- En la red publica como cualquiera tiene acceso a esta, es importante tener alguna lista que limite el acceso a ciertas direcciones IP y asi solo las especificadas tengan acceso, ademas de también solo tener abiertos los puertos necesarios y los demás cerrarlos. Es necesario también encriptar la información que pase a traves de la red publica a la aplicación.  
- En la base de datos es importante en esta tener una lista de acceso en donde se especifique desde donde se puede tener acceso a la base de datos. También especificar roles a los usuarios que tienen acceso a la base de datos, para después no tener inconvenientes y que solo ciertas personas puedan realizar ciertas acciones y otras no. También es bueno establecer contraseñas de acceso, que estén cambiando y solo las personas autorizadas tengan acceso a estas.  
- En la red privada es importante establecer un firewall eficiente que nos garantice protección en nuestra red privada y asi no permita el acceso de procedencias dudosas, asi como también detecte cualquier información que pueda intentar dañar nuestra base.  
- En general para la seguridad en el almacenamiento lo principal seria mantener los datos encriptados, para que en caso de que sean accedidos estos no puedan ser leídos, y de esta manera nos garantizamos que nuestros datos estén seguros.  

# Pregunta 4  

- ¿Por qué las bases de datos de series de tiempo son tan utilizadas en soluciones de Observabilidad? Realice un análisis desde el punto de vista de la naturaleza de los datos que se recolectan. (2 pts)  

Debido a que las bases de series de tiempo recolectan datos los cuales son ordenados por marcas en el tiempo es mucho mas sencillo utilizar esto para la observabilidad, ya que se puede ver por intervalos de tiempo como la información esta siendo procesada. Es mucho mas sencillo llegar a analizarla gracias a los intervalos de tiempo, por ejemplo, en caso de que se muestren datos en donde este llegando a fallar algo, se puede ver en que preciso momento fue el que comenzó a fallar y asi también se puede ver que solución se da. Ademas estas bases por lo general cuentan con herramientas como gráficos en tiempo real, que hacen que el análisis sea mucho mas sencillo como ya lo mencione antes.

- ¿Es posible utilizar BigTable como una base de datos de series de tiempo que se pueda utilizar como parte de una solución de Observabilidad? Justifique su respuesta desde el punto de vista de la naturaleza de la base de datos. (2 pts)  

BigTable puede manejar grandes volumenes de datos en tiempo real cada uno con un timestamp, lo que podría ayudarnos en una solución de observabilidad, y gracias a este mismo timestamp es que podríamos monitorear, analizar o recopilar datos en periodos de tiempo y podríamos llevar un control los datos por intervalos de tiempo. Sin embargo, no considero a BigTable como una base de datos de series de tiempo como tal, aunque si creo que se le puede llegar a dar un uso parecido, aprovechando este manejo en el tiempo que esta permite y asi darle una solución de observabilidad, aun asi, tampoco contara con todas las herramientas que cuentan las bases de series de tiempo.

- Suponiendo que tenemos una solución de Observabilidad que utiliza Elasticsearch, ¿Cómo podemos ahorrar dinero con información histórica? (2 pts)  

Una manera para ahorrar costos seria utilizar datos ordenados por el tiempo, en donde se defina un patron de tiempo para determinar que datos son mas relevantes que otros y asi asignar mayor espacio en memoria a los mas relevantes, los menos relevantes no se les asignara tanto espacio en memoria y solo se necesitaran en caso de ser accedidos.

- Comente las ventajas y las desventajas de utilizar un servicio de Observabilidad on-premise (por ejemplo, Prometheus y Grafana) vs un Managed Service (como Datadog), justifique su respuesta con la experiencia obtenida en la tarea corta 1 de este curso. (4 pts)  

- Servicios on-premise: 
  - Ventajas: Son una opción mas flexible y personalizada, en donde podemos modificar todo a nuestro gusto. Nosotros tenemos el control total sobre todo, podemos configurar todo para adaptarlo a lo que deseemos. Es una opción que no va a salir tan cara.  
  - Desventajas: Pueden llegar a ser complicadas de manipular y tediosas de configurar. Ademas al configurarlas nosotros mismos, debemos estar en constante revision de estas.  

- Managed Services:  
  - Ventajas: Son fáciles de configurar. Nosotros no nos encargamos de nada, mas que de pagar el servicio. Se pueden configurar alertas para que nos avisen en caso de alguna actividad en nuestra base de datos que sea de nuestro interés.  
  - Desventajas: Es una solución costosa, ya que se tendrá que estar pagando el servicio, asi como también estaríamos dependiendo de otros para la observabilidad en nuestro sistema. No son tan flexibles y personalizadas como los servicios on-premise, estas tal vez no nos permitan configurar mucho a nuestro gusto.

La verdad solo he tenido la oportunidad de probar un servicio on-premise el cual fue el que utilizamos en la tarea corta, y el uso de este no es tan complicado, pero tampoco es sencillo, se necesita su rato para poder configurarlo y lograr que funcione. No podría decir cual servicio es mejor, porque siento que tendría que probar un servicio managed, sin embargo, si me llama la atención un servicio managed debido a su simpleza, aunque no permite tanta flexibilidad o personalización en sus configuraciones.

# Referencias  

Avi. (2022, octubre 29). 7 Potente base de datos de series temporales para una solución de monitoreo. Geekflare. https://geekflare.com/es/time-series-database/  

Datadog. (s.f.). Alerting. Datadog Infrastructure and Application Monitoring. https://docs.datadoghq.com/monitors/

Kanade, V. (2022, noviembre 17). Una guía introductoria a los datos de series temporales. Geekflare. https://geekflare.com/es/time-series-data/

Itelligent. (2018, octubre 3). Usar Elasticsearch, ¿qué ventajas ofrece esta tecnología? ITELLIGENT. https://itelligent.es/es/ventajas-elasticsearch/