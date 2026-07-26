# Propuesta de Proyecto: Pipeline y API de Predicción de Precios con pisos.com

## 👥 Roles y Responsabilidades

### 🏗️ Data Architect

* **Responsable del Diseño en AWS:**
    - Definir y configurar la arquitectura en la nube, incluyendo el bucket S3, la base de datos **PostgreSQL en RDS** y los permisos de los servicios. Considerar el uso de proxies y servicios para escalar el scraping.

### ⚙️ Data Engineer

* **Responsable del Pipeline de Datos:**
    - Implementar los scripts de **web scraping** (usando herramientas como requests o httpx) para la extracción masiva inicial y la recolección diaria de anuncios inmobiliarios de pisos.com. Gestionar la carga, limpieza y transformación de estos datos desde S3 a la base de datos.

### 🔬 Data Scientist

* **Responsable del Análisis y Modelado:**
    - Diseñar la lógica para interpretar las preguntas en lenguaje natural del endpoint de Q&A enfocado al mercado inmobiliario.
    - Entrenar un modelo de machine learning (ej. regresión, XGBoost o transformers) para predecir el precio de un inmueble (compra o alquiler) o la tendencia de precios en una zona específica basándose en sus características (m², habitaciones, ubicación, etc.).

### 🚀 ML Engineer

* **Responsable del Despliegue y la API:**
    - Envolver la lógica de consulta y el modelo de predicción de precios en una API robusta utilizando FastAPI.
    - Desplegar la aplicación FastAPI en una instancia de AWS EC2, asegurando que todos los endpoints sean funcionales.

---

## 📝 Fases del Proyecto

### **Fase 01: Infraestructura y Pipeline de Datos (Web Scraping)**

**Objetivo:** Construir un sistema automatizado que extraiga datos de anuncios de inmuebles de pisos.com mediante web scraping y los almacene de forma estructurada en una base de datos **PostgreSQL**.

**Tareas Clave:**

1. **Extracción de Datos (Data Engineer, Architect):**
* Desarrollar la lógica de scraping para navegar por el portal.
* Crear un pipeline para realizar una extracción masiva de anuncios históricos/actuales y guardar el HTML crudo o los JSON extraídos en un **bucket S3**.
* Configurar un proceso recurrente (**AWS Lambda** con **EventBridge**) para que se ejecute diariamente y obtenga los nuevos anuncios o los cambios de precio de las últimas 24 horas.


2. **Procesamiento y Carga (Data Engineer, Architect):**
* Desarrollar una **AWS Lambda** que se active con un **trigger de S3** al recibir los nuevos ficheros del scraping.
* Esta función procesará los datos extraídos (parseando precios, metros cuadrados, ubicación, características), los limpiará y los cargará de forma estructurada en la base de datos **PostgreSQL**.


3. **Exploratory Data Analysis (EDA) Preliminar (Data Scientist)**:
* Conectarse a la base de datos PostgreSQL (o analizar directamente los crudos en S3) usando Jupyter Notebooks.
* Analizar la calidad de los datos inmobiliarios: detección de valores nulos, outliers (ej. errores tipográficos en precios o metros cuadrados, anuncios fraudulentos o duplicados).
* Identificar patrones de precios por zonas, correlaciones entre el precio y las características del inmueble (habitaciones, extras como piscina/garaje) y seleccionar las características (features) más relevantes. Este análisis servirá como base para el entrenamiento del modelo y para el diseño del dashboard en Streamlit.


**Entregables de esta fase:**

* Infraestructura en AWS (S3, RDS, contenedores/Lambda para scraping) configurada.
* Pipelines de web scraping automáticos (masivo inicial y actualización diaria) funcionando.
* Base de datos poblada, normalizada y actualizada con los inmuebles de pisos.com.

### **Fase 02: Modelado, API y Despliegue**

**Objetivo:** Desarrollar una API que permita consultar datos del mercado inmobiliario y predecir o estimar precios de viviendas.

**Tareas Clave:**

1. **Desarrollo del Modelo (Data Scientist):**
    - Utilizar los datos históricos y actuales extraídos para entrenar un modelo de predicción que estime el precio de un inmueble dado su código postal y características, o que realice un *forecasting* de la tendencia de precios en un barrio concreto.


2. **Desarrollo de la API (ML Engineer, Data Scientist):**
    - Crear una aplicación con **FastAPI** que incluya los siguientes endpoints:
        - `/ask`: Recibe una pregunta en texto (ej. *"Precio medio de un piso de 3 habitaciones en Madrid Centro"* o *"¿Dónde es más barato alquilar en Barcelona?"*), la interpreta, construye una consulta a la base de datos y devuelve la respuesta.
        - `/predict` (o `/forecast`): Recibe las características de un inmueble (ubicación, m², etc.) y devuelve la estimación de precio o la tendencia de mercado generada por el modelo.

3. **Despliegue (ML Engineer):**
    - Desplegar la aplicación FastAPI completa en una instancia **AWS EC2** para que sea accesible públicamente.

4. **Desarrollo de la Interfaz Web interactiva (Data Scientist, ML Engineer)**:
    - **Exploratory Data Analysis (EDA)**: Construir una aplicación en Streamlit que muestre un dashboard interactivo con visualizaciones de los datos inmobiliarios (ej. mapas de calor de precios por barrios, evolución temporal de los precios, distribuciones de tipologías de vivienda).
    - **Integración de la API**: Conectar la web de Streamlit con los endpoints de FastAPI para:
        - Proveer una barra de búsqueda/chat que permita al usuario hacer preguntas en lenguaje natural sobre el mercado inmobiliario (consumiendo `/ask`).
        - Crear un simulador o tasador virtual donde el usuario introduzca los datos de una vivienda para visualizar gráficamente su valor estimado en el mercado actual (consumiendo `/predict`).


**Entregables de esta fase:**

* Un modelo de predicción/estimación de precios entrenado y evaluado.
* API funcional desplegada con los dos endpoints implementados.
* Documentación de la API (generada por FastAPI/Swagger).
* Dashboard interactivo en Streamlit accesible públicamente para explorar el mercado inmobiliario, ver mapas de precios y tasar viviendas.