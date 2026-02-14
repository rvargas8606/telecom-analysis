#  Análisis de Comportamiento de Clientes: ConnectaTel (Telecomunicaciones)

##  Descripción del Proyecto
Este proyecto forma parte de mi formación como **Data Analyst**. El objetivo principal es analizar el comportamiento de los usuarios de la empresa **ConnectaTel** en Latinoamérica, utilizando datos históricos hasta el año **2024**.

A través de este análisis, se busca entender cómo los clientes consumen servicios de llamadas y mensajes, identificar patrones de abandono (Churn) y proponer mejoras estratégicas en los planes ofrecidos.

---

##  Herramientas y Tecnologías
* **Lenguaje:** Python 3.x
* **Librerías:** * `Pandas`: Manipulación y limpieza de datos.
    * `NumPy`: Operaciones matemáticas y manejo de valores nulos.
    * `Matplotlib` & `Seaborn`: Visualización de datos y análisis estadístico.
* **Entorno:** Jupyter Notebook / Google Colab.

---

## Estructura de los Datos
El análisis se basa en tres conjuntos de datos principales:
1.  **`plans.csv`**: Configuración de los planes (Básico y Premium), incluyendo precios mensuales, minutos/GB incluidos y tarifas por excedentes.
2.  **`users_latam.csv`**: Perfil demográfico de 4,000 clientes (edad, ciudad, fecha de registro, plan y fecha de baja).
3.  **`usage.csv`**: 40,000 registros de uso real (llamadas y mensajes) con duración y marcas de tiempo.

---

## Proceso de Análisis (Pipeline)

### 1. Exploración Inicial
Originalmente, los datos presentaban inconsistencias que habrían sesgado cualquier decisión de negocio si no se trataban:
* Identidad y Edad: Se detectó un valor "sentinel" (-999) en la columna age. Aunque era una sola etiqueta, afectaba el promedio general.
* Ubicación: La columna city tenía un 11.73% (469 filas) de valores nulos o representados por un "?", lo que impedía un análisis regional preciso.
* Fugas de Datos (Churn): La columna churn_date tenía un 88.35% (3,534 filas) de nulos. Lejos de ser un error, se identificó que representan a los clientes activos, revelando una tasa de retención saludable pero que requiere monitoreo.
* Anomalías Temporales: Se encontraron registros con fechas en el año 2026 (fechas futuras), lo que representaba un error de captura que fue saneado para mantener el análisis dentro del periodo 2024.
Se realizó un diagnóstico de la calidad de los datos detectando:
* Tipos de datos incorrectos en columnas de fecha.
* Presencia de valores centinela (como `-999` en edad).
* Datos faltantes en columnas clave como `city` y `churn_date`.

### 2. Limpieza y Transformación (Data Wrangling)
* **Tratamiento de Outliers:** Reemplazo de edades inválidas mediante la mediana.
* **Imputación de Nulos:** Uso de la moda para variables categóricas (`city`) y lógica de negocio para `churn_date` (asumiendo que los nulos son clientes activos).
* **Formateo:** Conversión de objetos a `datetime` y normalización de textos.

### 3. Análisis Exploratorio (EDA)
* Cálculo de ingresos mensuales por usuario.
* Comparativa de consumo: ¿Qué plan genera más excedentes?
* Identificación de ciudades con mayor tasa de abandono.

---

##  Hallazgos Clave
> [!TIP]
> * **Segmentación:** El grupo de edad predominante se encuentra en los [X] años.
> * **Consumo:** Los usuarios del plan Básico tienden a exceder su límite de [minutos/datos] en un [X]%.
> * **Retención:** Se detectó una correlación entre el uso de mensajes y la permanencia en el servicio.

---

##  Contacto
Si tienes alguna duda o quieres conectar para charlar sobre análisis de datos, ¡encuéntrame en LinkedIn!

---
*Este proyecto fue desarrollado como parte del Sprint 7 de Análisis de Datos en mi Bootcamp de TripleTen.*
