[//]: # (Portada)
# Instituto Tecnológico de Costa Rica

# Escuela de Computación

# Bases de Datos II GR 1

# Apuntes Clase del 10 de marzo del 2023

# Estudiante: 
# Carlos Eduardo Leiva Medaglia / 2021032973

# Profesor: 
# Gerardo Nereo Campos Araya

# I Semestre 2023
[//]: # (Dejo esto para que el siguiente texto inicie en una nueva página)
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
# 
# 
# 

# Dudas sobre la Tarea
#### ¿Agregar Base de Datos? 

Para agregar otra base de datos, se debe copiar y pegar uno de los ejemplos de las bases de datos que se encuentran en el chart.yaml y simplemente remplazar los datos con los valores correspondientes para la base deseada. En este caso para MariaDB nada más se cambia la versión, se coloca el nombre y se le asigna el estado como enabled.  

![Apuntes](https://i.imgur.com/8aFkD0g.png)  
![Apuntes](https://i.imgur.com/1idsOvd.png)  

#### ¿Cómo agregar la función de monitoreo?
Elasticsearch empaquetado por bitnami no viene con la función de monitoreo activada, por lo que uno mismo va a tener que configurarlo. En values.yaml se crea una nueva categoría, en este caso para Elasticsearch, donde se agrega “Metrics” y el “Servicemonitor” estos dos por defecto están en false, por lo que se tienen que cambiar a true. Para cualquier paquete de bitnami este sería el proceso para activar la función de monitoreo.  

![Apuntes](https://i.imgur.com/1idsOvd.png)  

#### ¿Http conections desde Gatling hasta bases de datos que no exponían un Endpoint?
MariaDB utiliza el puerto 3306 como puerto predeterminado para conexiones. Este puerto expone un canal de comunicación que utiliza un formato definido por MariaDB para intercambiar bytes. En el lado del cliente, la aplicación necesita un conector que le permita comunicarse en el mismo lenguaje de bytes y formato definido por MariaDB para enviar y recibir datos. Por ejemplo, existe el conector de MariaDB para Python.  

![Apuntes](https://i.imgur.com/dJVM7gY.png)

Por otro lado, las bases de datos NoSQL se comunican a través de HTTP, utilizando un formato de intercambio de datos estandarizado en formato textual. HTTP se utiliza para conectarse a páginas web normales y define cómo se envía la información en formato de texto. Este protocolo define los verbos, siendo los más importantes GET, PUT, POST y DELETE. En las bases de datos existe el CRUD (acrónimo de Create, Read, Update y Delete), el cual se mapea directamente con los verbos de HTTP. En cualquier lugar donde se permita el uso de HTTP, este se relaciona con los puertos 80 y 443.  
Mientras que algunas empresas no permiten el acceso al puerto 3306, todas aceptan HTTP. Por esta razón, las bases de datos NoSQL utilizan protocolos basados en HTTP. De esta manera, CREATE equivale a PUT, READ a GET, UPDATE a POST y DELETE a DELETE. Para ello, se utiliza un lenguaje universal llamado JSON. Al utilizar JSON y HTTP, las bases de datos NoSQL exponen un endpoint HTTP que se puede acceder desde un navegador web, y una aplicación que se conecta a esa base de datos solo necesita un cliente HTTP y no un formato estándar. 

![Apuntes](https://i.imgur.com/FvoV5dE.png)

Para realizar pruebas de carga sobre endpoints HTTP, se utiliza una herramienta llamada Gatling. Esta herramienta puede comunicarse con un endpoint como el de Elasticsearch, pero no puede hacerlo directamente con el de MariaDB. Para solucionar este problema, se necesita un API (por ejemplo, FASTAPI) que permita la comunicación entre Gatling y MariaDB, y que maneje los verbos necesarios para hacer queries. Gatling necesita realizar inserciones, para lo cual se envía la query a través de FASTAPI y se ejecuta en MariaDB. Esto funciona como un traductor entre Gatling, un endpoint HTTP y una base de datos MariaDB. Para hacer una llamada directa a un API, se pueden utilizar diferentes herramientas. Si se necesita hacer un POST y enviar un JSON, el API debería poder procesar y devolver la información correcta.  
![Apuntes](https://i.imgur.com/AsRExwp.png)

#### ¿Pruebas unitarias?
Las pruebas unitarias consisten en probar porciones del código de manera aislada para demostrar que ciertas partes funcionan correctamente. Es por eso por lo que en lugar de hacer prints para verificar partes del código, se realizan pruebas unitarias. En estas pruebas, se llama a una función con un valor esperado y se verifica si se devuelve lo mismo en diferentes ocasiones, siempre y cuando el algoritmo no cambie. En entornos corporativos en los que trabajan varias personas en un mismo código, se utilizan pruebas unitarias para verificar en caso de que algo falle, ya que la salida del algoritmo sería distinta a la esperada. De esta manera, si algo sale mal, otra persona puede identificar el problema y corregir el código afectado.  

Sin embargo, el testing no se limita a pruebas unitarias, sino que también abarca un ciclo de vida con diferentes tipos de pruebas, como unit test, smoke test, integration test, staging test y QA. En algunas industrias, como la médica, se sigue un proceso formal para verificar que el código funcione al 100%, ya que cualquier error podría tener consecuencias graves. Las pruebas unitarias permiten que el código sea más elegante y menos propenso a errores.   

![Apuntes](https://i.imgur.com/A5fn2lc.png)

En sistemas como Windows, las computadoras tienen características llamadas loopback, localhost y 127.0.0.1, todas están características apuntan a la misma máquina.  Un ejemplo de esto relacionado con orientación a objetos seria cuando se tiene un objeto “this”, este apunta al objeto actual y, por lo tanto, a sí mismo. Si se llama a una función, el “this” ya no apuntará a sí mismo, sino al objeto en el que se está ejecutando el código en ese momento. De manera similar, Docker build es un pequeño workstation que tiene sus propias características.  

Algunas personas tenían un MariaDB y una prueba unitaria que verificaba la conexión con Mariadb. Sin embargo, dentro del contenedor, esto no funcionaba ya que MariaDB no estaba instalado en el mismo, si no, en un workstation afuera. Es importante recordar que las pruebas deben ser adaptadas al entorno en el que se ejecutan.  

![Apuntes](https://i.imgur.com/oE4X52G.png)

# Nodo Máster, Ingest y Data en Elasticsearch
Elasticsearch tiene tres tipos básicos de nodos: el nodo máster, el nodo data y el nodo ingest. El nodo máster es el coordinador del clúster y supervisa la salud de este. Además, es el encargado de decidir hacia dónde se dirigen los datos cuando se almacenan. Los nodos ingest son nodos especializados que actúan como pipelines de transformaciones de datos, pueden ser tan simples como convertir una fecha a otro format. Cuando una solicitud de inserción o indexación de datos entra en los nodos ingest, estos se encargan de transformar los datos antes de enviarlos al nodo data para su almacenamiento. Los nodos data son los nodos especializados en realizar operaciones CRUD en el clúster.  

![Apuntes](https://i.imgur.com/40msjiy.png)

Por lo general, los nodos ingest ingresan los datos y los nodos data los almacenan. Aunque se puede realizar una inserción en un nodo máster o en cualquier otro nodo, esto no suele ser lo más optimo, ya que este tiene que coordinar con los nodos de ingest y de data para realizar la tarea, lo que resulta redundante y consume recursos innecesariamente. Por esto, las operaciones de inserción se realizan en los nodos de ingest, mientras que las operaciones de búsqueda se realizan en los nodos de data.  
![Apuntes](https://i.imgur.com/FsZQGSV.png)
Si el nodo máster se queda sin recursos, puede afectar el rendimiento de todo el clúster. Por lo tanto, es importante tener en cuenta la distribución de recursos en cada tipo de nodo y asegurarse de que el nodo máster tenga suficientes recursos para realizar sus funciones de coordinación adecuadamente.  

# Nodo Data y su distribución de Shards

En Elasticsearch, se puede tener un nodo data que contenga un índice y dentro de ese índice tener uno o varios shards. El problema con tener un solo nodo data es que se convierte en un punto de falla único y se convierte en un cuello de botella. Si se agregan dos nodos, se puede tener un shard primario y un shard secundario, lo que aumenta el rendimiento ya que los usuarios pueden realizar operaciones de búsqueda en dos servidores diferentes. Esto mejora la capacidad de lectura del sistema, pero la capacidad de escritura sigue siendo la misma, ya que solo el shard primario puede escribir.  

![Apuntes](https://i.imgur.com/GhFNshH.png)

Si el shard primario comienza a crecer, los recursos físicos pueden convertirse en un problema, ya que se necesitará más memoria, etc. Por lo tanto, si se tienen dos nodos, se crearán dos shards por nodo, dos primarios y dos secundarios, lo que implica que los datos se dividirán en dos porciones de igual tamaño. Por ejemplo, si tenemos 100 GB de datos, se dividirán en 50 GB cada uno. El problema es que ambos shards primarios se encuentran en el mismo servidor, lo que genera dos puntos de falla. Eso no quiere decir que si el servidor donde se encuentran los shards primarios falla, el otro no se hará cargo. Es decir, existe un failover, como ambos shards primarios están en el mismo servidor, el tiempo en recuperar dos shards no es lo mismo que recuperar uno solo.  

![Apuntes](https://i.imgur.com/PqspT3L.png)

Por lo tanto, lo ideal es tener shards primarios en diferentes nodos o servidores para mejorar la disponibilidad y la tolerancia a fallos del sistema. Las ventajas de tener shard primarios y secundarios distribuidos entre dos nodos son varias:  

-	Se divide la carga de escritura entre dos nodos, lo que mejora el rendimiento sin necesidad de añadir más hardware.
-	Al tener dos shard secundarios en nodos diferentes, se divide el 50% de las lecturas, lo que permite pedir datos a cualquiera de los nodos disponibles. 
-	Las búsquedas se pueden realizar en paralelo en ambos shards secundarios, lo que aumenta el rendimiento al trabajar en dos servidores simultáneamente.  

![Apuntes](https://i.imgur.com/W4zF9hf.png)

Cuando se hacen muchas particiones, si se realiza una búsqueda, el sistema utiliza muchos recursos y necesita mucha coordinación, por lo tanto, en lugar de tener dos shards, podríamos tener tres shards, cada uno con alrededor de 35GB de las 100GB que se tienen en datos. Esto divide el trabajo que cada shard debe realizar, por lo que las operaciones deberían mejorar.  
Cuando se realiza una búsqueda, esta se reparte entre todos los nodos que tienen réplicas secundarias. No solo las secundarias se encargan de esto, ya que los nodos máster están preguntando constantemente qué nodos tienen réplicas, y los nodos les van dando feedback, en caso de que el uso de memoria este muy alto, podría llegar a realizarse la búsqueda en un shard primario.  
De igual manera no se gana nada con la partición de datos porque se redujo el trabajo que tenía un solo nodo. Si se hubieran usado las tres particiones en un solo nodo, este tendría menos trabajo, pero otro nodo agarraría más trabajo, lo que haría que el tiempo de ejecución aumente. A través de la observabilidad, nos damos cuenta de esto.  

![Apuntes](https://i.imgur.com/4qXFQen.png)

Si se agrega un nuevo nodo y se crea un nuevo índice, se puede hacer una distribución adecuada de los shards que estaban anteriormente en los otros dos nodos, lo que aumentaría considerablemente la capacidad del sistema tanto para escritura como para lectura en todos los nodos.  

![Apuntes](https://i.imgur.com/a22BLss.png)

Si se guía bajo la idea de divide y vencerás y se llegara a agregar otro servidor y no se agregan shards, los nodos maestros de Elasticsearch deberán redistribuir los shards (shard relocation). Al hacer esto, se organizarán los datos de una manera más inteligente. Pero al hacerlo, se podría llegar a tener el mismo problema, ya que los shards primarios podrían estar en tres servidores y este servidor extra no aporta ninguna ventaja. Además, podría recargar el trabajo de las búsquedas en un solo nodo.  

![Apuntes](https://i.imgur.com/VnokufI.png)

Otro caso, dos data nodes, un índice, dos shards, uno primario y secundario. Si el sistema tiene low writes y high searches. Al escribir poco, tener dos shards primarios está bien, pero el tiempo de respuesta está cayendo porque los nodos no son suficientes para manejar toda la cantidad de búsquedas que están pidiendo.  

![Apuntes](https://i.imgur.com/vdACoUh.png)

Se agregan replicas y como los shards son pequeños, se agregan replicas en los nodos. Esto no va a funcionar porque estaríamos utilizando el mismo hardware para hacer ese trabajo, tendría sentido si se agregan un par de servidores más, donde cada servidor tendría shards secundarios, replicando la información. Esto generaría que el trabajo se divida en varios servidores, por lo que, si una solicitud de información llega, la información de un usuario puede ser buscada desde cualquier servidor.    

Esto logra aumentar el rendimiento, pero se están desperdiciando recursos, por el simple hecho de que los datos son muy pequeños y se dejan dos servidores sin utilización. Entonces, se utilizan tres replicas, lo que hará que cada uno de los servidores mejore el rendimiento porque cada uno manejará un 25% de los datos. No se busca partición de datos en shard primarios, pero sí replicación de datos, ya que hay pocos writes, muchos search. No se garantiza la consistencia entre los queries iguales que realicen los clientes. La escritura de los shard primarios debe distribuirse entre todos los nodos, por lo que hay un tiempo en el que no esté actualizado los datos. Por lo que un shard puede estar actualizado y otro puede que no, lo que puede generar resultados inconsistentes.  

![Apuntes](https://i.imgur.com/yWclzCL.png)

# Datos Ordenados por Tiempo
Las bases de datos NoSQL o SQL de gran escala manejan datos que siguen un patrón de tiempo. A medida que se acercan a la hora actual, son más relevantes, y a medida que pasan menos tiempo, son menos relevantes. Los datos se dividen en categorías de hot, warm, cold, frozen y glacier. Los usuarios suelen consumir principalmente los datos "hot", y no están interesados en buscar datos antiguos. Por ejemplo, Twitter no muestra los mismos tweets de hace años, sino que muestra los tweets más recientes.  

![Apuntes](https://i.imgur.com/53qo7RB.png)

Cada dato se va a acceder de distintas maneras, por lo que se asigna una proporción de memoria diferente para cada tipo de dato. En un mundo ideal, la memoria sería tan grande como el disco lo que evitaría tener que moverse al disco para buscar datos. Sin embargo, esto es muy costoso. Por lo tanto, se dividen las relaciones y a cada tipo de dato por cada gigabyte de memoria se le asigna una cantidad de disco, de esta manera:  

-	Hot: por cada gigabyte de memoria, se asignan 30 GB de disco.
-	Warm: por cada gigabyte de memoria, se asignan 60 GB de disco.
-	Cold: por cada gigabyte de memoria, se asignan 90 GB de disco.
-	Frozen: por cada gigabyte de memoria, se asignan 120 GB de disco.
-	Glacier: No se le asigna memoria.

![Apuntes](https://i.imgur.com/ZubIn8f.png)

Lo más importante en un sistema distribuido es que todos los nodos sean iguales, independientemente de los datos que contengan. Las bases de datos NoSQL no pueden tener el mismo hardware para todos los usuarios, ya que, si hay datos "Cold" en servidores exactamente iguales que los "Hot", estos últimos acapararían el uso del servidor "Hot", dejando al otro servidor sin utilizar.  
Es importante definir el porcentaje de datos de cada categoría y definir instancias para cada tipo de datos. Las bases de datos NoSQL ofrecen un bajo costo y alto rendimiento. A medida que los datos se alejan de la hora actual, se van moviendo a diferentes niveles de datos. Content, hot, warm, cold o frozen. Content son los datos que los usuarios suelen buscar y siempre quieren tener disponibles, estos requieren mucha memoria y CPU. Hot tiene muchas lecturas y moderadas escrituras. Warm tienen lecturas moderadas y bajas escrituras. Cold tiene lecturas esporádicas y prácticamente no tiene escrituras, estos solo se usan en modo de solo lectura, con unas 10 o 20 búsquedas al mes. Cuando los datos están frozen se utiliza lo que se llama un file system. También se utiliza el object storage, que es una interfaz HTTP que expone los mismos verbos y permite escribir, actualizar, etc. Los datos en frozen se encuentran en el object storage, que se encuentra en un archivo que se busca en la red, por lo tanto, este se busca, se pone en el servidor, se monta, se hace la búsqueda, y después se desmonta, a estas búsquedas se les llama fully mounted indexes y estas son sumamente caras.  

![Apuntes](https://i.imgur.com/OQJB5u7.png)



