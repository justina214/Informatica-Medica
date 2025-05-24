# Trabajo Práctico 4 - Informática en Medicina

## Integrantes
Franzi, Lucas
Imas Navarro, Justina

## Docentes

- Eugenia Uberrino
- Melina Piacentino

## Institución

## Parte 1

**Descripción**: Listar todos los pacientes registrados.
PARTE 1: Bases de Datos 
Base de datos centro médico 

Se desea diseñar una base de datos relacional que almacene la información sobre los pacientes, médicos, recetas y consultas en un centro de salud. En la actualidad, la gestión de esta información se lleva a cabo del siguiente modo: Cuando una persona acude al centro de salud, se le toma nota en una ficha con sus datos personales: nombre, fecha de nacimiento, sexo biológico y dirección (calle, número y ciudad). Esta ficha queda registrada en el archivo de pacientes del centro. Los médicos del centro también tienen su ficha, donde se registran su nombre completo, especialidad y dirección profesional. Cada vez que un médico realiza una consulta o tratamiento a un paciente, puede emitir una receta. Esta receta incluye la fecha, el nombre del paciente atendido, el médico que la emite, el medicamento o tratamiento indicado, y la enfermedad o condición que motivó la prescripción. Esta información queda registrada y organizada para facilitar tanto el seguimiento del paciente como las auditorías clínicas. Los tratamientos pueden incluir medicamentos, indicaciones como reposo o fisioterapia, y suelen tener especificaciones temporales (por ejemplo, “tomar por 5 días” o “uso indefinido”). También se registran enfermedades o diagnósticos asociados, permitiendo análisis estadísticos o seguimiento epidemiológico. 

El sistema busca reemplazar los registros en papel por una solución digital que permita realizar búsquedas rápidas, obtener estadísticas de distribución demográfica, sexo y especialidad, y mantener la información organizada para su integración con otros módulos médicos como historiales clínicos, turnos o recetas médicas. 

Nota: La implementación hecha por la cátedra de esta base de datos está en el archivo previamente compartido “base_de_datos.sql”. 
Consignas: 
1. ¿Qué tipo de base de datos es? Clasificarla según estructura y función. 
2. Armar el diagrama entidad-relación de la base de datos dada. 
3. Armar el modelo lógico entidad-relación de la base de datos dada. 
4. ¿Considera que la base de datos está normalizada? En caso que no lo esté, ¿cómo podría hacerlo? Nota: no debe normalizar la base de datos, solo explicar como lo haría. 

**EJERCICIO 1**
La clasificacion segun la estructura es RELACIONAL porque esta organizada en tablas que se relacionan entre si mediante claves que pueden ser primarias o foraneas
Clave primaria: campo que identifica univocamente a un registro. Puede ser una clave primaria simple o una clave primaria compuesta.

Clave foránea: campo que hace referencia a la clave primaria de otra tabla, estableciendo una relación entre ellas
La clasificacion segun su funcion es transaccional, las cuales se usan para gestionar datos dinamicos y operativos del día a día en un sistema de atención médica (registro de pacientes, médicos, consultas, etc.).

**EJERCICIO 2**

![Descripción de la imagen](ejercicio%202.png)

Entidades:
-Pacientes
- *id_paciente* (PK) SERIAL  #Primary Key de la tabla, que identifica de forma única a cada paciente. SERIAL indica que es un número que se autoincrementa.
- nombre VARCHAR(100)
- fecha_nacimiento DATE
- id_sexo (FK) INT #Clave foránea que hace referencia a la tabla de sexo. 
- numero VARCHAR(10)
- calle VARCHAR(100)
- ciudad VARCHAR(100)
-Medicos
- *id_medico* (PK) SERIAL
- nombre VARCHAR(100)
- especialidad_id (FK) INT
- telefono VARCHAR(15)
- email VARCHAR(100)
- matricula INT
-Consultas
- *id_consulta* (PK) SERIAL
- id_paciente (FK) INT
- id_medico (FK) INT
- fecha DATE
- diagnostico TEXT
- tratamiento TEXT
- snomed_codigo BIGINT
- UNIQUE(fecha, id_medico, id_paciente, snomed_codigo)
-SexoBiologico:
- *id_sexo* (PK) INT
- descripcion VARCHAR(50) UNIQUE
-Especialidades
- *id_especialidad* (PK) SERIAL
- nombre VARCHAR(100) UNIQUE
-Recetas
- *id_receta* (PK) SERIAL
- fecha DATE
- id_medico (FK) INT #Clave foránea que hace referencia a la tabla de médicos. Indica quién emitió la receta.
- id_paciente (FK) INT
- id_medicamento (FK) INT
- descripcion TEXT
- UNIQUE(fecha, id_medico, id_paciente, id_medicamento)
Relaciones:
-Un paciente tine un SexoBiologico pero un SexoBiologico puede estar relacionado a muchas pacientes, entonces queda de la forma:
Pacientes (N) ← → (1) SexoBiologico
-Un Medico tiene una Especialidad pero una Especialidad puede tener muchos médicos, entonces la relacion es de la forma:
Medicos (N) ← → (1) Especialidades
-Una consulta se realiza por un Médico y es para un Paciente, entonces por un lado, un paciente puede tener muchas consultas pero una consulta corresponde a exactamente un paciente y queda de la forma 
Consultas (N) ← → (1) Pacientes
Por otro lado, un medico puede realizar muchas consultas pero una consulta es realizada por exactamente un medico
Consultas (N) ← → (1) Medicos
Por ultimo, un paciente puede tener muchas recetas, y una receta corresponde a exactamente un paciente
Recetas (N) ← → (1) Pacientes
Un medico puede realizar muchas recetas, pero una receta es dada por un solo medico
Recetas (N) ← → (1) Medicos
Una receta tiene un medicamento pero a su vez un medicamente puede estar en muchas recetas
Recetas (N) ← → (1) Medicamentos

**EJERCICIO 3** Modelo Lógico Entidad-Relación (Modelo Relacional)

Tablas con claves:
SexoBiologico(id_sexo PK, descripcion UNIQUE)


Pacientes(id_paciente PK, nombre, fecha_nacimiento, id_sexo FK, numero, calle, ciudad)


Especialidades(id_especialidad PK, nombre UNIQUE)


Medicos(id_medico PK, nombre, especialidad_id FK, telefono, email, matricula)


Consultas(id_consulta PK, id_paciente FK, id_medico FK, fecha, diagnostico, tratamiento, snomed_codigo, UNIQUE(fecha, id_medico, id_paciente, snomed_codigo))

**EJERCICIO 4** ¿Está normalizada la base de datos?

La base de datos está parcialmente normalizada. A continuación, se explica cómo evaluarla en términos de las primeras tres formas normales (1FN, 2FN, 3FN):
Primera Forma Normal (1FN):
Cumple. Todas las tablas tienen campos atómicos (sin listas, conjuntos o campos repetidos).
Segunda Forma Normal (2FN):
Cumple. No hay dependencias parciales porque todas las tablas tienen claves primarias simples (o seriales), y los atributos no clave dependen completamente de la clave primaria.
Tercera Forma Normal (3FN):
No cumple totalmente.
 Hay redundancia y dependencia transitiva:
En la tabla Pacientes, los campos calle, numero y ciudad podrían estar normalizados en una tabla separada de direcciones para evitar datos repetidos (por ejemplo, varias veces aparece “Calle San Juan” en Rosario).


Además, ciudad está escrita de formas inconsistentes ("Bs Aires", "Buenos Aires", "buenos aires", " Buenos Aires", etc.), lo que evidencia falta de integridad referencial y justifica una tabla Ciudades.


Para normalizar la tabla se sugiere lo siguiente:
Crear una tabla Direccion con campos id_direccion, calle, numero, ciudad, y luego referenciarla desde Pacientes.


Crear una tabla Ciudad para mantener consistencia y evitar entradas duplicadas con distintas grafías.


Agregar validaciones o restricciones que impidan datos duplicados como los dos pacientes llamados "Juan Pérez".



##Parte 2: SQL 

Consignas: 
1. Cuando se realizan consultas sobre la tabla paciente agrupando por ciudad los tiempos de respuesta son demasiado largos. Proponer mediante una query SQL una solución a este problema. 


```sql
SELECT * FROM Pacientes;
