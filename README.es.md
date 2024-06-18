Proyecto JOF
¡Hola a todos! Somos estudiantes del Bootcamp de Ciencia de Datos y Aprendizaje Automático: Javier Serrano, Olga Kurganova y Fernando Tejada. Para nuestro proyecto final, hemos decidido trabajar con un conjunto de datos que registra la energía recolectada por un panel solar en una ubicación geográfica específica. Además, el conjunto de datos incluye variables relacionadas con las condiciones climáticas, el tiempo cronológico y la variación en la cantidad de energía producida, todas las cuales pueden influir en la cantidad de radiación solar que el panel recoge, incluida la "Irradiancia Global Horizontal" (IGH).

Hello everyone! We are students of the Data Science & Machine Learning Bootcamp: Javier Serrano, Olga Kurganova, and Fernando Tejada. For our final project, we have decided to work with a dataset that records the energy collected by a solar panel in a specific geographical location. Additionally, the dataset includes variables related to weather conditions, chronological time, and the variation in the amount of energy produced, all of which can influence the amount of solar radiation the panel collects, including the "Global Horizontal Irradiance" (GHI).

## <span style="color:blue">Tabla de Contenidos</span>

1. [<span style="color:blue">Variables del Conjunto de Datos</span>](#variables-del-conjunto-de-datos)
2. [<span style="color:blue">Descripción del Proyecto</span>](#descripción-del-proyecto)
3. [<span style="color:blue">Configuración</span>](#configuración)
    - [<span style="color:blue">Prerrequisitos</span>](#prerrequisitos)
    - [<span style="color:blue">Instalación</span>](#instalación)
    - [<span style="color:blue">Crear una Base de Datos</span>](#crear-una-base-de-datos)
    - [<span style="color:blue">Variables de Entorno</span>](#variables-de-entorno)
4. [<span style="color:blue">Ejecutando la Aplicación</span>](#ejecutando-la-aplicación)
5. [<span style="color:blue">Añadiendo Modelos</span>](#añadiendo-modelos)
6. [<span style="color:blue">Trabajando con Datos</span>](#trabajando-con-datos)
7. [<span style="color:blue">Descripción de los Scripts</span>](#descripción-de-los-scripts)
8. [<span style="color:blue">Contribuciones</span>](#contribuciones)
9. [<span style="color:blue">Licencia</span>](#licencia)
10. [<span style="color:blue">Referencias</span>](#referencias)

## Variables del Conjunto de Datos

- `Time`                                      
- `Energy delta [Wh]`  **(target)**                        
- `GHI` (Global Horizontal Irradiance)        
- `Temp`                                     
- `Pressure`                                
- `Humidity`
- `Wind_speed`                                  
- `Rain_1h`                                  
- `Snow_1h`                                 
- `Clouds_all`                                
- `isSun_category`                                     
- `SunlightTime`                             
- `DayLength`                                 
- `SunlightTime/dayLength`                    
- `Weather_type`                             
- `Hour`                                     
- `Month`    



- `Time`                                      
- `Energy delta [Wh]`  **(target)**                        
- `GHI` (Global Horizontal Irradiance)        
- `Temp`                                     
- `Pressure`                                
- `Humidity`
- `Wind_speed`                                  
- `Rain_1h`                                  
- `Snow_1h`                                 
- `Clouds_all`                                
- `isSun_category`                                     
- `SunlightTime`                             
- `DayLength`                                 
- `SunlightTime/dayLength`                    
- `Weather_type`                             
- `Hour`                                     
- `Month`    

Gracias a este conjunto de datos, podremos crear un modelo de Aprendizaje Automático que nos permita determinar si la instalación de paneles solares es viable basándonos en la cantidad de energía que pueden recolectar (Energy delta [Wh]) y las condiciones climáticas en el sitio de instalación elegido. De esta manera, crearemos una herramienta que permita tanto a individuos locales como a empresas del sector energético verificar si es rentable invertir en la instalación de paneles solares.

Thanks to this dataset, we will be able to create a Machine Learning model that allows us to determine whether the installation of solar panels is viable based on the amount of energy they can collect and the weather conditions at the chosen installation site. In this way, we will create a tool that enables both local individuals and energy sector companies to verify whether it is profitable to invest in the installation of solar panels.

## Configuración

**Prerrequisitos**

Asegúrate de tener Python 3.11+ instalado en tu máquina. También necesitarás pip para instalar los paquetes de Python.

**Instalación**



Navega hasta el directorio del proyecto e instala los paquetes de Python requeridos:

```bash
pip install -r requirements.txt
pip install optuna
```

**Optuna utiliza técnicas de optimización más avanzadas, como la optimización bayesiana, que permite explorar el espacio de búsqueda de hiperparámetros de manera más eficiente que GridSearch. Optuna ajusta dinámicamente su búsqueda según los resultados observados, lo que conduce a una convergencia más rápida hacia la mejor combinación de hiperparámetros. Por otra parte, GridSearch realiza una búsqueda exhaustiva en una cuadrícula predefinida, lo que puede ser prohibitivamente costoso en términos de tiempo y recursos computacionales en espacios de búsqueda grandes.**

**Optuna ofrece una paralelización eficiente para la evaluación de múltiples configuraciones de hiperparámetros, lo que puede acelerar significativamente el proceso de búsqueda. GridSearch, por otro lado, no es tan eficiente en términos de paralelización y puede ser más lento en comparación, especialmente en conjuntos de datos grandes o en espacios de búsqueda complejos.**

*Optuna utilizes more advanced optimization techniques, such as Bayesian optimization, which allows for exploring the hyperparameter search space more efficiently than GridSearch. Optuna dynamically adjusts its search based on observed results, leading to faster convergence towards the best combination of hyperparameters. On the other hand, GridSearch performs an exhaustive search over a predefined grid, which can be prohibitively expensive in terms of time and computational resources in large search spaces.*

*Optuna offers efficient parallelization for evaluating multiple hyperparameter configurations, which can significantly speed up the search process. GridSearch, on the other hand, is not as efficient in terms of parallelization and may be slower in comparison, especially on large datasets or complex search spaces.*

**Creamos una base de datos**

Crea una nueva base de datos dentro del motor Postgres personalizando y ejecutando el siguiente comando: `$ createdb -h localhost -U <username> <db_name>`
Conéctate al motor Postgres para usar tu base de datos, manipular tablas y datos: `$ psql -h localhost -U <username> <db_name>`
NOTA: Recuerda revisar la información del archivo ./.env para obtener el nombre de usuario y db_name.

¡Una vez que estés dentro de PSQL podrás crear tablas, hacer consultas, insertar, actualizar o eliminar datos y mucho más!

**Variables de entorno**

Crea un archivo .env en el directorio raíz del proyecto para almacenar tus variables de entorno, como tu cadena de conexión a la base de datos:

```makefile
DATABASE_URL="your_database_connection_url_here"
```

## Ejecutando la Aplicación

Para ejecutar la aplicación, ejecuta el script app.py desde la raíz del directorio del proyecto:

```bash
cd src
python -m streamlit run app.py
```

## Añadiendo Modelos

Para añadir clases de modelos SQLAlchemy, crea nuevos archivos de script de Python dentro del directorio models/. Estas clases deben ser definidas de acuerdo a tu esquema de base de datos.

Definición del modelo de ejemplo (`models/example_model.py`):

```py
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import Column, Integer, String

Base = declarative_base()

class ExampleModel(Base):
    __tablename__ = 'example_table'
    id = Column(Integer, primary_key=True)
    name = Column(String)

```

## Trabajando con Datos

Colocamos  nuestros conjuntos de datos brutos en el directorio data/raw, conjuntos de datos intermedios en data/interim, y los conjuntos de datos procesados listos para el análisis en data/processed.

Para procesar datos, modificamos el script app.py para incluir tus pasos de procesamiento de datos, utilizando pandas para la manipulación y análisis de datos.

## Contribuyentes

Esta plantilla fue construida como parte del [Data Science and Machine Learning Bootcamp](https://4geeksacademy.com/us/coding-bootcamps/datascience-machine-learning) de 4Geeks Academy por [Alejandro Sanchez](https://twitter.com/alesanchezr) y muchos otros contribuyentes. Descubre más sobre [los programas BootCamp de 4Geeks Academy](https://4geeksacademy.com/us/programs) aquí.

Otras plantillas y recursos como este se pueden encontrar en la página de GitHub de la escuela.