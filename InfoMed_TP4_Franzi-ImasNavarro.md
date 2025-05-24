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

EJERCICIO 1
La clasificacion segun la estructura es RELACIONAL porque esta organizada en tablas que se relacionan entre si mediante claves que pueden ser primarias o foraneas
Clave primaria: campo que identifica univocamente a un registro. Puede ser una clave primaria simple o una clave primaria compuesta.

Clave foránea: campo que hace referencia a la clave primaria de otra tabla, estableciendo una relación entre ellas
La clasificacion segun su funcion es transaccional, las cuales se usan para gestionar datos dinamicos y operativos del día a día en un sistema de atención médica (registro de pacientes, médicos, consultas, etc.).
EJERCICIO 2



```sql
SELECT * FROM Pacientes;
