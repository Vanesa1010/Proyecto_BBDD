# Proyecto de base de datos académica

## 1. Contexto y problemática

Partimos de cinco archivos CSV: cuatro correspondientes a clases y uno al claustro. La información de alumnos, profesores, campus, verticales, promociones y evaluaciones estaba repartida entre distintos archivos. Esto dificultaba relacionar los datos, evitar duplicidades y obtener una visión global de la actividad académica.

## 2. Objetivo

Diseñar una base de datos relacional que centralice la información, facilite su consulta y permita incorporar nuevos datos a medida que crezca la organización. La solución debe poder utilizarse tanto en local como desde aplicaciones externas.

## 3. Enfoque del equipo

Abordamos el problema de forma progresiva: analizamos los archivos de origen, identificamos las entidades y sus relaciones, diseñamos el modelo, preparamos los datos con Python y desarrollamos su implementación en PostgreSQL. El equipo exploró distintas formas de trasladar el diseño conceptual a tablas concretas, manteniendo el mismo objetivo común.

## 4. Modelo entidad-relación

![Diagrama entidad-relación del equipo](modelo_ER.png)

El diagrama conceptual identifica ocho entidades principales:

| Entidad | Información que representa |
| --- | --- |
| Profesor | Personal docente |
| Modalidad | Forma de impartición de la enseñanza |
| Campus | Sedes de la organización |
| Vertical | Área formativa |
| Promoción | Convocatoria o edición académica |
| Alumno | Estudiantes matriculados |
| Proyecto | Actividades evaluables de cada vertical |
| Evaluación | Resultado de un alumno en un proyecto |

El modelo conecta al profesorado con campus y modalidades, las promociones con campus y verticales, los alumnos con promociones y las evaluaciones con alumnos y proyectos. El paso al modelo lógico permite concretar estas relaciones mediante claves y, cuando sea necesario, tablas intermedias.

El diagrama es una representación conceptual compartida, no un listado exhaustivo de las tablas de cada implementación. Las cardinalidades y restricciones definitivas deben corresponder al modelo lógico que se entregue.

## 5. Transformación y normalización

Utilizamos Python y pandas para leer los CSV, unificar la información de las clases, homogeneizar los campos, separar las entidades y generar identificadores. Reorganizamos las calificaciones para poder relacionar cada alumno con sus proyectos.

La normalización busca evitar información repetida, almacenar valores individuales en cada campo y separar los datos que pertenecen a entidades distintas. Las claves primarias identifican cada registro y las claves foráneas conectan las tablas. La comprobación de las formas normales depende de las claves y dependencias del modelo lógico definitivo.

## 6. Implementación en PostgreSQL

Creamos las tablas y sus relaciones mediante instrucciones SQL. Después incorporamos los datos preparados con pandas, respetando el orden de las dependencias entre tablas. Utilizamos restricciones para evitar duplicados y referencias a registros inexistentes.

El entorno local permitió desarrollar y comprobar la solución antes de trasladarla al servidor remoto.

## 7. Despliegue en Render

Utilizamos Render como plataforma de alojamiento de PostgreSQL. La conexión desde Python se realiza mediante psycopg2 o SQLAlchemy, utilizando los parámetros del servidor y el nombre de la base de datos correspondiente.

El despliegue permite consultar la información desde distintos equipos sin depender del ordenador en el que se desarrolló el proyecto. Cuando se prueban diferentes implementaciones en un mismo servidor, deben utilizarse bases de datos independientes para evitar conflictos entre tablas y registros.

No se incluyen credenciales en esta documentación. Deben configurarse de forma privada, preferiblemente mediante variables de entorno.

## 8. Consultas y utilidad práctica

Desarrollamos consultas SQL para responder preguntas como:

- ¿Cuántos alumnos hay por campus y vertical?
- ¿Cómo se distribuyen los estudiantes entre promociones?
- ¿Qué porcentaje de evaluaciones son aptas por proyecto?
- ¿Cómo se organiza el claustro por sede, modalidad y área formativa?
- ¿Qué alumnos han superado los cinco proyectos de su itinerario actual?

Estas consultas muestran cómo una base de datos organizada facilita la extracción de información útil para la gestión académica.

## 9. Tecnologías utilizadas

- Python y pandas: preparación y transformación de los datos.
- Jupyter Notebook: desarrollo y documentación del proceso.
- PostgreSQL y SQL: almacenamiento, relaciones y consultas.
- psycopg2 y SQLAlchemy: conexión entre Python y PostgreSQL.
- pgAdmin: administración y revisión de la base de datos.
- Render: alojamiento remoto.
- GitHub: colaboración y documentación del proyecto.

## 10. Reproducción del proyecto

1. Preparar un entorno Python con pandas, SQLAlchemy y psycopg2-binary.
2. Ejecutar el proceso de transformación sobre los CSV originales.
3. Configurar una base PostgreSQL vacía y sus parámetros de conexión.
4. Ejecutar la creación de tablas y la ingesta correspondientes a la implementación elegida.
5. Ejecutar las consultas de demostración.

Si se entregan scripts SQL independientes, estos permiten crear la estructura e insertar los datos directamente en PostgreSQL sin repetir la transformación en Python. No deben ejecutarse sobre una base ya cargada sin revisar previamente su contenido.

## 11. Escalabilidad y mejoras futuras

El diseño busca facilitar la incorporación de nuevos campus, verticales, modalidades, promociones, alumnos y proyectos. Como posibles ampliaciones se plantean la gestión de aulas, el historial de asignaciones docentes, la automatización de la ingesta y la conexión con herramientas de visualización.

La incorporación de aulas y la gestión temporal detallada del profesorado requieren información adicional que no está disponible en los archivos de origen. Estas mejoras no se presentan como funcionalidades ya implementadas.

## 12. Conclusión

Hemos abordado el paso de archivos dispersos a una solución relacional organizada, consultable y accesible remotamente. El proyecto combina diseño de bases de datos, transformación de información, programación y despliegue en la nube, estableciendo una base para futuras aplicaciones de gestión y análisis académico.

## Autores

IÑAKI GALLEGO, VANESA TURIEL, OSCAR SOLANO, ORTZI SAMANIEGO
