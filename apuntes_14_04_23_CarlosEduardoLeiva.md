[//]: # (Portada)
# Instituto Tecnológico de Costa Rica

# Escuela de Computación

# Bases de Datos II GR 1

# Apuntes Clase del 14 de abril del 2023

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

[//]: # (![] imagen)
# Rendimiento en la Base de Datos
Algunos conceptos importantes en cuanto al rendimiento de la base de datos son:  
- Scan: El scan en terminos generales y en SQL  es una busqueda secuencial. Si su dataset tiene N cantidad de registros lo que va a causar en el peor de casos es que tiene que hacer N busquedas. Scan puede considerarse uno de los peores enemigos en el rendimiento.  
![Apuntes](https://imgur.com/ko70ZF8.png)  
- Search: Tiene una estructura llamada indice, en donde dice exactamente donde esta guardado en el disco la informacion que se busca. Es importante que los indices puedan entrar en memoria principal, ya que este tiene que hacer el procesamiento rapido, si el indice no cabe en memoria principal va a traer del disco paginas de memoria. Esto lo que puede hacer es que cuando esta haciendo la busqueda que representa el indice, el procesador puede no encontrar el dato y genera un page fold a nivel de memoria y necesita ir a disco a traer los datos, lo que puede generar problemas en el rendimiento.  
![Apuntes](https://imgur.com/1CkfzmG.png)  
- Blob (Big Large Objects): es un objeto muy grande para tener en la base de datos, sobre todo en una relacional, como videos por ejemplo. Estos archivos por lo general, son guardados en un Static Content Repository,estos generan una URL para el archivo, lo que permite que en la base se guarde el URL de la ubicacion del archivo.Se usan los CDN (Content Delivery Networks), que son para almacenar informacion estatica y generar URLs.  
![Apuntes](https://imgur.com/VkG48J1.png)    
- Metadatos: son los datos de los datos, por ejmplo: Salio una cancion de Red Hot Chili Peppers, un metadato de la cancion es pasar el audio a texto y usar el texto, los autores, los vocalistas, etc.  

> Cuando tenemos Blob's podemos aplicar tecnicas como OCR (reconocimiento de texto en imagenes). Tecnica Speech to text (Convertir audo en texto), entre otras. Todas estas tecnicas nos permiten meter los datos en la base de datos.  

Ejemplo de uso de Blob: En pandemia surgian muchas recetas propias caseras para tratar COVID, las farmaceuticas hacian mucho analisis para buscar sustancias que podian ayudar. A una farmaceutica se le ocurrio comprar todos los strings de comentarios y tweets que se generaban, a esto le hacia analisis de entidades para identificar productos que podian tratar covid de forma casera. Tenia base de datos para los remedios caseros y los medicamentos y los comparaba, para extraer sustancias en comun. Cosas que se pueden hacer con bases de datos y Blops.
# Formas Normales
## Primera Forma Normal  

Tenemos que mantener valores atomicos en todos los campos.  
Por ejemplo, una persona puede tener dos telefonos pero estos no pueden estar separados por coma, deben estar en campos atomicos, por lo que deberiamos tener dos filas, cada una con un numero telefonico distinto.  
> Valores multievaluados a valores atomicos.  

![Apuntes](https://imgur.com/o0DUuVZ.png)  
En el ejemplo tenemos problemas porque hay duplicidad, osea mas almacenamiento y los indices generan problemas, porque serian indices mas grandes. En el ejemplo podria ser mas rapido hacer querys de la forma incorrecta, pero esto no garantiza consistencia en nuestra BD.
## Segunda Forma Normal  
Los atributos que no son parte de una llave dependen de forma completa del primarykey, elimina dependencias parciales.  

![Apuntes](https://imgur.com/fPPhVoD.png)  

> SELECT * FROM DetalleCompra AS DT INNER Articulo AS A ON  DT.id_articulo = A.id_Articulo where #factura = '365'

El query anteior podria ser un ejempo de una consulta que se realizaria una vez aplicada la forma correcta en las tablas. Esto podria ser una penalizacion en el rendimiento, ya que, necesitariamos alrededor de 4 indices, necesitariamos un indice en Articulo de la tabla DetalleCompra, uno en numero de factura, uno para la primary key y otro para el articulo en la tabla Articulo.  
A la hora de ejecutar el query, este terminara realizando subconsultas usando los diferentes indices para lograr el resultado, por lo que, si lo tuvieramos como antes solo haria una busqueda sola y daria el resultado, en terminos de rendimiento es mas rapido, pero tiene implicaciones, como puede ser duplicidad de datos.
![Apuntes](https://imgur.com/hR5zUPf.png) 
![Apuntes](https://imgur.com/kMx6gMa.png)  
## Tercera Forma Normal  
Dependencia de forma no transitiva de la clave primaria. Todos los subconjuntos de atributos que no forman parte de la clave primaria. Esto trae el mismo problema que el segundo, penalizacion en el rendimiento.  

![Apuntes](https://imgur.com/bzDEQF9.png)  

> Al tener una recuperacion de datos costosa en rendimiento, el cliente tiene una penalizacion en que tan rapido obtiene la informacion, por eso ponemos en una balanza que tanto queremos tener normalizada la base y despues vemos el dinero que queremos invertir en la solucion. Si perdemos usuarios por los retrasos vamos a tener que meter mas hardware poara logar mantener los tiempos de respuestas, si crece en usuarios hay que meter mas hardware, si uno no normaliza completamente no cumplimos con el modelo relacional, pero tenemos tiempos de respuesta es mas rapido.
# Indices  
## Como funcionan los datos?
En un archivo de datos se guarda un registro de datos, que representa una fila en una base de datos. Los datos se guardan al final del archivo (Heap) y puede generar que algunos datos se borren, lo que haria que queden espacios vacios en el archivo, por lo que hay que desfragmentar (movimientos de datos), esto lo comenzaron a implemnetar las bases de datos. 
Cada registro que se guarda en la base se guarda junto con una estructura paralela que indica donde esta la localizacion del archivo. Esto permite que si se realiza un scan, nos podemos mover a traves de esa estructura para encontrar el archivo deseado.  
![Apuntes](https://imgur.com/LhID0gE.png)  
Existen registros de tamano variable y tamano estatico. En uno estatico siempre todos los registros lucen iguales (cada campo tiene la misma cantidad de bytes), mientras que el variable no.  
En un esquema de tamano estatico la fragmentacion del archivo es facil de manejar porque nada mas se mantiene un registro de espacios libres y cuando se guarda un registro nuevo se ve si hay espacios libres y de ser asi, se guarda en el espacio libre.  
![Apuntes](https://imgur.com/uGXoixm.png)  
En el variable se tiene primero todos los registros que son estaticos, como el id, despues se tiene un metacampo, que es el size del campo que es variable, si hay otro campo que es de tamano variable se debe agregar otro campo size.  
![Apuntes](https://imgur.com/KRxgIHB.png)  
Si se ocupa borrar se complica, porque debe haber una forma de poder darle continuidad a los registros, por lo que debriamos agregar tambien dentro del registro un next, que dice a donde arranca el siguiente registro.  
![Apuntes](https://imgur.com/flW3p0y.png)   
![Apuntes](https://imgur.com/8lubD0U.png)  
> El tipo de registro que se utilice va a depender del workload y el comportamiento de la base de datos.  
## Indices
- Clustered Index: Incrustar el indice dentro del archivo de datos. Se genera una estructura que va a estar incrustada dentro del archivo de datos. La estructura de datos (un arbol) va a tener en las hojas los archivos que estamos buscando.  
![Apuntes](https://imgur.com/RB4o2pL.png) 
- Non-Cluster Index: Tenemos un archivo de datos y cada uno de los registros tiene n Cantidad de columnas y tenemos un indice para cada columna, por lo que tendriamos multiples archivos que dentro del archivo tendra una estructura definidia y esos archivos tendran esas estructuras y tendran solo la informacion necesaria para armar el indice. Entre mas indices tengamos bien definidos las lecturas se incrementan pero entre mas indices mas duran las escrituras.  
![Apuntes](https://imgur.com/i7apSkF.png) 
- Clustered and NonClustered: Podemos tener un cluster index y multiples noncluster.
- Expression Index: Permite indexar expresiones, lo que nos permite indexar resultados de operaciones.  
![Apuntes](https://imgur.com/LOs0QYg.png) 
- Partial Index: Es un indice que esta enfocada solo en una parte especifica de una tabla. Puede traer un mejor rendimiento en las consultas que cubran la parte de la tabla del indice, sin embargo, si se hace una consulta que cuenta con una parte de la tabla que no esta cubierta por el indice no va a ser util.  






