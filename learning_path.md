# RUTA DE APRENDIZAJE: DE INGENIERO DE SISTEMAS A DATA ENGINEER (OPENSIGNAL)

Esta ruta está diseñada para aprovechar tus bases en **Ingeniería de Sistemas**, desarrollo y bases de datos, utilizando **Agentic AI** (Claude y Antigravity) como acelerador de aprendizaje y desarrollo, con el objetivo de cubrir el 100% del stack de Opensignal (Scala, Spark, SQL, Redshift, Athena, S3, Airflow, EMR).

---

## ESTRATEGIA DE APRENDIZAJE CON AGENTIC AI (TU SUPERPODER)
Dado que usas **Claude** y **Antigravity**, tu método de estudio no será leer manuales de 500 páginas, sino **aprender haciendo (hands-on) guiado por IA**.
*   **Prompting para aprender:** Pídele a Antigravity: *"Explícame [Concepto X] usando analogías de administración de sistemas que ya conozco del sistema integral que construí".*
*   **Generación de código y tests:** Escribe el código en borrador y pídele a la IA: *"Genera la prueba unitaria en ScalaTest para este código y explícame paso a paso cómo funciona".*
*   **Explicación de errores:** Cuando un script falle, copia el error en la IA para hacer **Análisis de Causa Raíz (Root Cause Analysis)**, que es un requisito clave del empleo.

---

## FASE 1: SCALA Y PRUEBAS UNITARIAS (Semanas 1 y 2)
**Objetivo:** Transicionar de la programación imperativa/orientada a objetos tradicional (Java/PHP/C#) a la **Programación Funcional** en Scala.

### 1. Conceptos Clave de Scala:
*   `val` (inmutable) vs `var` (mutable) — En Scala y Spark, la inmutabilidad es regla de oro.
*   Tipos de datos básicos y colecciones (`List`, `Map`, `Seq`, `Set`).
*   Funciones de orden superior: `map`, `filter`, `flatMap`, `foldLeft`, `reduce`.
*   Pattern Matching y `Option` (`Some` / `None` para evitar excepciones de puntero nulo).
*   Clases de caso (`case class`) para modelar esquemas de datos.

### 2. Configuración de Entorno:
*   Instalar Java JDK (versión 11 o 17).
*   Instalar **sbt** (Scala Build Tool).
*   Configurar VS Code con la extensión **Metals** o usar IntelliJ IDEA Community.

### 3. Pruebas Unitarias (Unit Testing):
*   Aprender el framework **ScalaTest**.
*   *Práctica diaria:* Escribir funciones de procesamiento lógico y escribir sus respectivos casos de prueba (Happy path, Edge cases, Empty lists).

---

## FASE 2: SQL AVANZADO, AWS S3 Y ATHENA (Semanas 3 y 4)
**Objetivo:** Dominar el almacenamiento de datos moderno y consultas eficientes sobre "Data Lakes".

### 1. SQL Avanzado para Data Analytics:
*   Funciones de ventana (`ROW_NUMBER()`, `RANK()`, `LEAD()`, `LAG()`, `SUM() OVER(...)`).
*   Common Table Expressions (CTEs) con `WITH` para estructurar consultas complejas.
*   Agregaciones complejas y optimización de índices/joins.

### 2. AWS S3 como Data Lake:
*   Conceptos de almacenamiento en la nube, buckets, prefijos (carpetas virtuales).
*   Formatos de archivo eficientes: **Parquet** (columnar) vs CSV/JSON (fila).

### 3. AWS Athena (Presto):
*   Creación de tablas externas que apuntan a archivos en S3.
*   Particionamiento de tablas en Athena para ahorrar costos y acelerar consultas.
*   Consultar datos estructurados y semi-estructurados (JSONs anidados) usando SQL.

---

## FASE 3: APACHE SPARK CON SCALA (Semanas 5, 6 y 7)
**Objetivo:** Aprender a procesar gigabytes/terabytes de datos usando procesamiento distribuido.

### 1. Arquitectura de Spark:
*   Driver, Executors, Cluster Manager.
*   Lazy Evaluation (Transformaciones vs Acciones).
*   DAG (Directed Acyclic Graph) en Spark.

### 2. Programación con Spark DataFrames y Datasets:
*   Lectura de datos semiestructurados (JSON, CSV, logs).
*   Transformaciones básicas: `select`, `filter`, `groupBy`, `join`, `withColumn`.
*   Uso de `Dataset[T]` (tipado fuerte en Scala) utilizando tus `case class`.

### 3. Optimización y Buenas Prácticas:
*   Evitar el "Shuffle" innecesario (intercambio de datos entre nodos).
*   Broadcast Joins para unir tablas pequeñas con tablas grandes.
*   Manejo de "Data Skew" (desbalance de datos en particiones).
*   Escribir pruebas unitarias para transformaciones de Spark usando **Spark Session Testing**.

---

## FASE 4: AWS EMR, REDSHIFT Y ORQUESTACIÓN CON AIRFLOW (Semanas 8 y 9)
**Objetivo:** Desplegar y automatizar flujos de trabajo de datos en la nube.

### 1. AWS EMR (Elastic MapReduce):
*   Cómo aprovisionar clusters de Hadoop/Spark en AWS.
*   Ejecutar aplicaciones Spark en EMR (`spark-submit` o EMR Steps).
*   Monitorear ejecuciones usando Spark UI.

### 2. AWS Redshift:
*   Conceptos de Data Warehouse columnar.
*   Distribution Keys (Distkeys) y Sort Keys para optimizar tablas masivas.
*   Carga de datos desde S3 a Redshift usando el comando `COPY`.

### 3. Apache Airflow:
*   Creación de DAGs (Directed Acyclic Graphs) en Python.
*   Operadores básicos: `BashOperator`, `PythonOperator`.
*   Operadores de AWS: Lanzar y apagar clusters EMR desde Airflow (`EmrCreateJobFlowOperator`, `EmrAddStepsOperator`).

---

## FASE 5: PROYECTO INTEGRADOR FIN DE RUTA (Semana 10)
**Objetivo:** Construir un proyecto portafolio que demuestre todas las habilidades requeridas por Opensignal.

### El Proyecto: "Telecomp Market Analytics Pipeline"
1.  **Datos de entrada:** Un conjunto de datos JSON crudos simulados con registros de velocidad de red móvil (coincidiendo con el foco de Opensignal).
2.  **Almacenamiento inicial:** Guardar el JSON crudo en AWS S3.
3.  **Procesamiento:** Un script de Spark en Scala que:
    *   Lee los JSON de S3.
    *   Limpia datos nulos y filtra registros inválidos.
    *   Calcula métricas: Promedio de velocidad de bajada/subida agrupados por operador móvil y coordenadas geográficas.
    *   Escribe el resultado optimizado en formato Parquet particionado por operador.
    *   *Debe incluir pruebas unitarias completas escritas en ScalaTest.*
4.  **Data Warehouse:** Carga automática de los datos procesados en tablas de AWS Athena o Redshift.
5.  **Orquestación:** Un DAG de Airflow que programa esta tarea diariamente y envía alertas en caso de fallo.

---

## PLAN DE ACCIÓN INMEDIATO (DÍA 1)
1.  **Crea tu Workspace:** Abre el directorio del proyecto `C:\Users\iitsupportmx\.gemini\antigravity\scratch\opensignal-career-prep` como tu espacio de trabajo en tu editor de código.
2.  **Instala Java y sbt** en tu sistema.
3.  **Inicia tu primer laboratorio de Scala:** Pídele a Antigravity en una nueva consulta: *"Estoy en la Fase 1. Ayúdame a crear un proyecto básico de Scala con sbt, configurar ScalaTest y escribir mi primera prueba unitaria"*.
