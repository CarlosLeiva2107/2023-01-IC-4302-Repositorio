[//]: # (Portada)
# Instituto Tecnológico de Costa Rica

# Escuela de Computación

# Bases de Datos II GR 1

# Prueba Corta #9

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
[//]: # (Resolución Quiz)
1. Suponiendo que un sistema de bases de datos relacional que presenta un read-heavy
workload y los queries son muy diferentes, explique detalladamente ¿porque el uso
de caches puede afectar el rendimiento del sistema de forma negativa? (30 pts)  

Cuando se tiene un read-heavy workload  y queries diferentes el uso del cache puede afectar el rendimiento de forma negativa por varias razones. Una de estas es que puede generarse inconsistencia en los datos, ya que en caso de que se modifiquen datos en la base de datos, y estos cambios no se vean reflejados en la cache, al realizar una consulta si esta obtiene la información de la cache obtendrá resultados incorrectos. También, la ventaja del uso de la cache, es no traer los datos de disco, esto puede ser beneficioso con consultas similares, pero al ser consultas diferentes, siempre serian distintas y por esto mismo es que podría haber inconsistencia si se trae los datos de la cache. De igual manera, como se menciono antes, en caso de que se actualicen datos, para que todo este coherente, se necesita actualizar los datos también en la cache, esta actualización puede generar una perdida de tiempo. Un gran problema es que se puede dar perdida de datos, esto porque el tamaño de la cache es limitado y en caso de que se este eliminando datos en cache para aumentar su tamaño y esos datos sean consultados en ese momento antes de que se actualice la cache, puede haber una perdida de datos. por esas razones es que la cache puede afectar el rendimiento de forma negativa.

2. El particionamiento de tablas en bases de datos relacionales es un concepto muy
parecido al de shards en bases de datos NoSQL, explique detalladamente ¿Cómo
afecta el particionamiento y el sharding en el rendimiento de bases de datos SQL y
NoSQL? (30 pts)  

En bases de datos SQL el particionamiento de tablas puede ser beneficioso gracias a que los datos pueden estar distribuidos de una forma mas ordenada y con una buena estructura que es lo que se busca con bases SQL. Asi mismo, se mejora la escabilidad, ya que como dije los datos pueden estar distribuidos, lo que trae una mejor escabilidad. Sin embargo, yo considero, que al particionar las tablas, esto puede traer problemas de rendimiento en consultas muy largas, donde se necesite obtener información de varias tablas, ya que tendría que verificar la información en muchísimas tablas, por lo que se debe realizar correctamente.  

El sharding también puede ser muy beneficioso, ya que al hacer sharding podemos distribuir cargas de trabajo entre distintos shards, lo que también trae una mejora en la estabilidad. De igual manera se aprovecha el paralelismo ya que con el sharding podemos ejecutar consultas al mismo tiempo en diferentes shards. El sharding es beneficioso en caso de que se tenga un workload muy especifico, ya que se puede agregar shards de solo lectura por ejemplo, y de esta manera si se tienen muchas consultas de lectura estas responderán mas efectivamente. Sin embargo, como lo mencione con el particionamiento, esto se debe hacer correctamente para no traer perdidas en el rendimiento.  

3. En un sistema de bases de datos con Strong Consistency cuyo workload es de
read-heavy y write-heavy, ¿Cómo afectan los exclusive locks el rendimiento de las
bases de datos NoSQL? (20 pts)  

El rendimiento puede ser afectado de manera negativa por varias razones. Entre ellas puede ser que se de un bloqueo en las lecturas y las escrituras, ya que cuando se de un exclusive lock, puede ser que se bloquee por un determinado tiempo y que otros procesos de escritura o lectura no sean permitidos lo que ocasionaría retrasos en la ejecución de operaciones. También puede haber momentos en los que se den bloqueos mutuos, lo que ocasionaría un impacto negativo en el tiempo de espera. Los locks también puede ser difíciles de manejar conforme crece la base de datos, y teniendo en cuenta que esta tiene read-heavy y write-heavy, es una base de datos que esta en constante uso y por lo mismo puede estar en crecimiento.

4. Explique detalladamente, ¿Cómo afecta la selección de discos físicos el rendimiento
de una base de datos SQL y NoSQL? (20 pts)  

La selección de los discos físicos tiene un gran impacto en el rendimiento de nuestras bases. Primeramente, este sera la unidad de almacenamiento, por lo que, dependiendo de la capacidad de este es la cantidad de datos que podrán estar almacenados, de la misma manera el tiempo en el que los datos tarden leyéndose o escribiéndose esta dado por el disco, y su tiempo de respuesta a estas dos operaciones. No es lo mismo un disco que cuente con una transferencia de datos de 80MB/s en operaciones de lectura y escritura a uno que cuenta con 175MB/s. Hay discos que cuentan con cache implementada, por lo que es bueno conocer la cantidad y la calidad de la cache implementada, para asi evitar problemas de rendimiento. También hay que tener en cuenta en caso de que se quiera implementar un RAID, ya que se debe saber que nivel de RAID se desea implementar y también, ver que discos usar para este RAID. Por esas razones es que escoger el disco físico en la base de datos es un paso muy importante y a tener enj cuenta para conseguir el mejor rendimiento en nuestra base.