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


1. Explique en que consisten los siguientes conceptos:  
    a. Data Warehouse  
    b. Data Lake  
    c. Data Mart  

a) Un Data Warehouse es un almacen de datos, que se utiliza para un analisis rapido de cantidades masivas de datos. Los datos en este deben ser almacenados de forma segura, fiable y facil de administrar. Un Data Warehouse es utilizado a niveles empresariales.  

b) Data Lake es un repositorio diseñado para procesar y proteger grandes cantidades de datos estructurados y no estructurados. Estos datos pueden estar en su forma original, por lo que no necesitan pasar por una transformacion previa. Los Data Lakes suelen estar configurados en un cluster, este puede existir de manera local o en la nube.  

c) Data Mart es una version simple de un Data Warehouse el cual esta enfocada en una area especifica. A nivel empresarial se puede tener Data Mart para cada subdivision de la empresa, lo que puede traer beneficios si se necesita extraer datos sobre algo en concreto. Los Data Marts son simples y faciles de administrar aunque la distribucion de los datos tambien podria traer problemas al estar divididos por sectores.  

2. ¿De que forma se benefician las aplicaciones del uso de Columnar Storage? Explique.  

Las aplicaciones se benefician de estas cuando se trata de consultas de solo lectura ya que sólo tienen que leer las columnas a las que se accede desde el disco o desde la memoria, esto hace que se reduzca el tiempo de acceso a los datos y aumenta el rendimiento de las consultas. Ademas, permiten una compresión más eficiente de los datos, ya que cada bloque físico contiene el mismo tipo de datos, lo que permite el uso de algoritmos de compresión muy eficientes. Esto ahorra espacio de almacenamiento y reduce la cantidad de operaciones necesarias para acceder a los datos. 

3. ¿En que consiste streaming y batch processing?  

Streaming implica la captura, almacenamiento y procesamiento de datos en tiempo real. El streaming les permite a las companias tener una amplia visibilidad en muchos aspectos sobre su negocio. Batch processing se trata de un metodo en el cual se procesan grandes cantidades de datos por lotes. Hay varios tipos de realizar el batch processing, entre estos pueden ser: Extract-Transform-Load, Extract-Load-Transform y Online Analytical Processing. El streaming se puede usar para monitoreo de datos en tiempo real como por ejemplo la salud de los pacientes de un hospital, mientras que el batch processing podria usarse para analizar datos sobre ventas al final del dia de un negocio, este ultimo no tiene que ser en tiempo real.  

4. ¿En que consiste datos estructurados, semi estructurados y no estructurados?  

Los datos estructurados son datos organizados en un esquema fijo y definido, como en una base de datos relacional, donde los datos se almacenan en tablas con columnas y filas definidas. Los datos semi-estructurados son aquellos que no siguen un esquema fijo, pero tienen una estructura definida, como los documentos XML o JSON. Los datos no estructurados son aquellos que no tienen una estructura definida, como imágenes, audio, video o texto libre.

Los datos estructurados son aquellos que cuentan con un esquema definido e inalterable, como las bases relacionales, las cuales siguen un esquema fijo y tiene sus maneras concretas para almacenar los datos.
Los datos semi-estructurados son aquellos que no tienen un esquema fijo pero su estructura es la misma
