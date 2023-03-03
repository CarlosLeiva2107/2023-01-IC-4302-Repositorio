[//]: # (Portada)
# Instituto Tecnológico de Costa Rica

# Escuela de Computación

# Bases de Datos II GR 1

# Prueba Corta #1

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
# 
# 
# 
# 
#  
#  
#  
#  
[//]: # (Resolucion Quiz)

1.	Explique cómo afectan los siguientes componentes el rendimiento de un sistema de base de datos:  
    a. Disco  
    b. Memoria Virtual  
    c. Memoria  
    d. Caché de CPU  
    e. CPU  

a) El disco es la unidad física de almacenamiento del computador, por lo que este tiene guardado absolutamente todos los datos relacionados con la base de datos. También, el disco puede ser encargado de realizar operaciones de lectura y escritura, por lo que un disco de mayor velocidad mejoraría estas operaciones. Sin embargo, el disco también puede tomarse tiempo en realizar estas operaciones, lo que traería consecuencias a la efectividad de nuestra base de datos.  

b)	Como lo dice el nombre, la memoria virtual no es como tal una unidad que se encuentre físicamente en el computador, básicamente es un espacio el cual simula la memoria principal. Al simular la memoria puede mejorar el rendimiento de la base de datos al poder tener mas datos en esta memoria y no tener que realizar todo el proceso de ir y leerlos del disco, simplemente busca en la memoria virtual. Cuando la base esta consumiendo mas memoria principal de la disponible, se va a agarrar de la memoria virtual para compensar la falta de la principal. La memoria virtual es mas lenta que la memoria principal, por lo que también podría generar problemas en los tiempos que se manejan en la base.  

c)	La memoria principal se dice que es el segundo componente más importante, después del CPU. La memoria puede mejorarnos el rendimiento de nuestra base de datos bastante ya que, si se garantiza que los índices de la base puedan estar completos en nuestra memoria principal, traería una reducción del uso del disco, esto generara que toda la información este en memoria principal, por lo que seria mucho mas rápido. Entre mas memoria principal poseamos más efectividad tendremos.  

d)	El cache es una memoria temporal que puede almacenar datos los cuales son usados repetitivamente. Esto ayuda de manera que, si la base utiliza unos datos de manera muy repetitiva, podrían ser guardados en cache, lo que nos facilitara el acceso a la hora de volverlos a necesitar ya que no tendrá que ir a buscar de disco, lo que aumentara la velocidad de acceso a datos. La cache también le quitaría carga al disco ya que no tendría que estar realizando operaciones de lectura ni escritura.  

e)	La CPU es el componente más importante ya que este es el encargado de gobernar todo lo relacionado con el computador. Dependiendo de como manejemos nuestra base de datos puede que el CPU este más presente o menos presente. El CPU se va a encargar de realizar todas las operaciones relacionadas a nuestra base, por lo que un CPU mas potente va a traer mayor efectividad. El CPU al ser la cabeza del computador, en caso de no realizar los procesos correctamente, puede perjudicar también a los demás componentes del computador.  

2.	¿De qué forma se benefician las aplicaciones del uso de caches? Explique.  

Como lo mencione anteriormente la cache es una memoria temporal que puede guardar datos repetitivos. Por lo que en palabras sencillas, a la hora de que las aplicaciones necesiten acceder a datos, estos pueden ser accedidos de manera más rápida por medio de la cache a diferencia de realizar todo el proceso de búsqueda de los datos en el disco. El uso de la cache va a traer una mejora en el rendimiento, ya que como lo mencione antes, los datos no necesitaran ser buscados en todo el disco ya que estarán en la cache, esto también traerá una mejora en el consumo de la energía. Como se puede ver, en lo que mas se pueden beneficiar las aplicaciones es que van a mejorar sus tiempos de ejecución porque cuando se necesite acceder datos que están en cache lo hará de manera mucho mas rápida, lo que mejorara la experiencia para el usuario también.  

3.	Desde el punto de vista de Elasticsearch, ¿Que es un índice?  

Un índice en Elasticsearch es una colección optimizada de documentos. Cada uno de estos documentos tendrá su propio identificador único, de tal manera que nos permite realizar búsquedas específicas. Elasticsearch también da la posibilidad de configurar la forma en que se pueden buscar estos documentos, a lo que me refiero con esto, es que se puede agregar maneras en las que nos permite realizar la búsqueda de manera mas especificas de acuerdo a lo que nosotros hayamos asignado. Básicamente los índices son estructuras las cuales nos van a permitir manipular de una mejor manera nuestros datos en Elasticsearch.  
4.	¿Qué es un mapping en Elasticsearch?  

El mapping básicamente nos permite describir la manera en la que los documentos de un índice deberán ser indexados. Elasticsearch nos otorga la posibilidad de definir  esto de manera automática o si se desea, se puede especificar como pueden ser analizados los campos, a lo que me refiero con esto, es que si se tiene un campo de tipo texto, se puede especificar de que manera quiere que sea analizado, esto nos ayudaría por ejemplo si trabajamos con formatos de fecha personalizados. El mapping va a ser muy importante ya que nos va a impactar en la forma en la que realizamos la búsqueda de nuestros datos y los resultados que obtendremos.  
