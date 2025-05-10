## API para Predicción de Especies de Iris

Esta API utiliza modelos de machine learning entrenados con el dataset Iris para predecir la especie de una flor de iris. El dataset contiene datos sobre diferentes variedades de la planta iris, y la API permite realizar predicciones ingresando las cuatro características principales de una flor:

* Largo del sépalo
* Ancho del sépalo
* Largo del pétalo
* Ancho del pétalo

Se pre-entrenarán cuatro modelos de clasificación distintos, y se almacenarán en archivos (como .h5) para su uso posterior por la aplicación. Cada modelo estará asociado a un endpoint diferente dentro de la API, permitiendo al usuario seleccionar el algoritmo para realizar la predicción:

* Regresión Logística
* Árbol de Decisión
* Máquina de Vectores de Soporte (SVM)
* Bosque Aleatorio (Random Forest)

### Archivos y Estructura del Proyecto

Se requiere la siguiente estructura de archivos:

\`\`\`
machine\_\_learning\_api/
├── models/
├── requirements.txt
├── iris\_models.py
└── app.py
\`\`\`

Donde:

* \`models/\`: Contiene los modelos pre-entrenados.
* \`requirements.txt\`: Lista las dependencias del proyecto.
* \`iris\_models.py\`: Contiene el código para entrenar y guardar los modelos de machine learning.
* \`app.py\`: Contiene el código de la aplicación Flask que define la API.

### Instalación

1.  Crear un entorno virtual de Anaconda (Python).
2.  Navegar al directorio \`machine\_\_learning\_api\`.
3.  Instalar las dependencias:

    \`\`\`
    pip install -r requirements.txt
    \`\`\`

### Modelos de Machine Learning

Ejecutar el script \`iris\_models.py\` para generar los modelos de machine learning:

\`\`\`
python iris_models.py
\`\`\`

### Ejecutar la API

Para iniciar el servidor de la API, ejecutar:

\`\`\`
python app.py
\`\`\`

La API se ejecutará en el puerto 5001.

### Probar la API

Para probar la API, se puede utilizar Postman u otra herramienta similar. Se deben enviar solicitudes POST a los siguientes endpoints, proporcionando los valores de las características de la flor de iris en el cuerpo de la solicitud (e.g., en formato JSON):

* \`/predict/logistic\`
* \`/predict/decisiontree\`
* \`/predict/svm\`
* \`/predict/randomforest\`

**Ejemplo de datos para la prueba (JSON):**

\`\`\`json
{
    "sepal_length": 5.1,
    "sepal_width": 3.5,
    "petal_length": 1.4,
    "petal_width": 0.2
}
\`\`\`

### Docker

#### ¿Qué es Docker?

Docker es una plataforma que permite:

* Empaquetar una aplicación y sus dependencias en una imagen.
* Ejecutar esa imagen en contenedores, que son unidades estandarizadas que se pueden ejecutar en cualquier sistema que tenga Docker instalado.
* Asegurar que la aplicación se comporte de la misma manera en diferentes entornos (desarrollo, pruebas, producción), eliminando el problema de "en mi máquina funciona".

#### Dockerización de la API

Para facilitar la implementación y el despliegue, se pueden utilizar Docker y Docker Compose. Se deben agregar los siguientes archivos a la carpeta \`machine\_\_learning\_api\`:

* \`Dockerfile\`: Contiene las instrucciones para construir la imagen de Docker para la API.
* \`docker-compose.yml\`: Define los servicios que conforman la aplicación (en este caso, solo la API) y cómo se deben ejecutar.

#### \`docker-compose.yml\`

Docker Compose es una herramienta que permite definir y ejecutar aplicaciones multi-contenedor con Docker, utilizando un único archivo de configuración (\`docker-compose.yml\`). Es ideal para aplicaciones que constan de varios servicios.

#### Levantar la API con Docker

1.  Abrir Docker Desktop.
2.  Ejecutar el siguiente comando en la terminal, dentro de la carpeta \`machine\_\_learning\_api\`:

    \`\`\`
    docker-compose up --build
    \`\`\`

    Este comando construye la imagen de Docker (si es necesario) e inicia el contenedor.

### Deployar la API en Producción con Render

Para desplegar la API en producción usando Render, seguir estos pasos:

1.  Agregar \`gunicorn\` al archivo \`requirements.txt\`:

    \`\`\`
    flask
    scikit-learn
    joblib
    gunicorn
    \`\`\`

2.  Crear una cuenta en Render (<https://render.com/>).
3.  Registrarse en Render (Sign Up o Sign In).
4.  En el panel de control de Render (<https://dashboard.render.com/>), hacer clic en el botón "+" y seleccionar "Web Service".
5.  En "Source Code", seleccionar "Connect to a Git Repository" y vincular la cuenta de GitHub.
6.  Buscar y seleccionar el repositorio que contiene el código de la API.
7.  Dar un nombre al servicio web.
8.  Seleccionar "Python" como el entorno.
9.  Verificar que la rama sea "main" o la rama donde se encuentra el código.
10. Verificar que los comandos de construcción (Build Command) e inicio (Start Command) sean correctos (Render los detecta automáticamente, pero es bueno verificar).
11. Seleccionar el plan gratuito.
12. Hacer clic en "Deploy Web Service".
13. Una vez que el servicio web esté desplegado, visitar la URL proporcionada por Render para acceder a la API.
