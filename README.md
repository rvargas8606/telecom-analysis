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

### Segmentación y Comportamiento por Edad
Identificamos tres segmentos claros:

Adultos Maduros (46-50 años): Es nuestro segmento más grande. Muestran un comportamiento estable y son la base principal de ingresos.

Usuarios Senior (60-80 años): Sorprendentemente activos, lo que indica que la interfaz o el servicio es accesible para ellos.

Jóvenes (20-30 años): Un segmento con menor presencia en la base actual, pero con un uso más intensivo de datos (proyectado por el bajo uso de SMS).

### Segmentos más Valiosos
El segmento más valioso actualmente es el Usuario del Plan Básico con Excedentes.

¿Por qué? Representan el 64.8% de la base. Aunque pagan una renta baja ($12), los usuarios que superan los 100 minutos de llamadas generan un margen de ganancia adicional por minuto que es más rentable proporcionalmente que el Plan Premium.

### Patrones Extremos (Outliers) y sus Implicaciones
Encontramos un grupo de 31 "Heavy Users" que consumen más de 100 minutos mensuales (llegando hasta 155 min).

Implicación: Estos usuarios están en el límite del Plan Básico o subutilizando el Plan Premium. Para el negocio, representan un riesgo de fuga si encuentran una oferta "Ilimitada" en la competencia, o una oportunidad de Upselling (subirlos de plan) si se les ofrece un paquete intermedio.

## Recomendaciones Estratégicas
Lanzamiento de un "Plan Connecta Medio": Existe un vacío enorme entre los 100 min ($12) y los 600 min ($25). Se recomienda un plan de $18 USD con 250 minutos, diseñado específicamente para capturar a los "outliers" del plan básico.

Rediseño del Plan Premium: El uso de SMS es casi nulo (promedio de 5 mensajes). El Plan Premium ofrece 500, lo cual no tiene valor real para el cliente. Recomendamos cambiar esos SMS por más GB de navegación, lo que justificaría mejor el precio de $25.

Campaña de Retención Regional: Dado que el 43% de los clientes están en Bogotá y CDMX, cualquier mínima mejora en la calidad del servicio en estas ciudades impactará masivamente en la reducción del Churn.
---

---
*Este proyecto fue desarrollado como parte del Sprint 7 de Análisis de Datos en mi Bootcamp de TripleTen.*
