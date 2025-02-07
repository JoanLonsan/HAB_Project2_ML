# PROYECTO 2

## GRUPO A

### ORIGEN DE DATOS

Importamos los datos de la [web AQICN](https://aqicn.org/) utilizando su API de exportación.

![alt AQICN](./images/Screenshot%20from%202024-07-05%2019-04-08.png)

### ESTUDIO

Descargamos los datos 4 veces cada día sobre el estado de calidad del aire en diferentes estaciones meteorológicas. Se recogen:
* Ozono (O3)
* Dióxido de Nitrógeno (NO2)
* Dióxido de Azufre (SO2)
* Monóxido de Carbono (CO)
* Temperatura, Presión
* Humedad, Proporción de Partículas Finas (PM2.5)
* Proporción de Partículas Respirables (PM10)
* Índice de Calidad del Aire (AQI, que se calcula a partir de los datos anteriores)
* Clase de Calidad del Aire (en función del valor AQI, se categoriza en una palabra/color fácil de leer)

Preparamos estos datos, y hacemos las pruebas con los diferentes algoritmos, obteniendo los dos mejores, guardando los resultados para re-utilizarlos en producción.

Finalmente, le presentamos al modelo/validación los datos leídos en la propia web de AQI actuales, y nos informará de la predicción que hace para el siguiente rango horario, tanto con un SCORE (AQI) como una clase (indicador de calidad).

### ALCANCE

Creemos que se trata de un estudio muy interesante, e incluso aplicable con pocos cambios y/o mejoras a una producción real.

#### ÁREAS DE MEJORA

Sería interesante realizar un análisis similar, pero añadiendo uno ( dos) NEXT_SCORE y NEXT_CLASS días más a cada lectura. Creemos que estos datos le darían más capacidad de predicción a los diferentes modelos. O incluso, con más código (y tiempo), se podría poner un formulario de selección de estación meteorológica, que leería el estado actual de la misma, y si en el CSV final añadiéramos los últimos datos como (PREVIUS_SCORE y PREVIUS_CLASS o incluso 2nPREVIUS_SCORE...), se obtendrían predicciones rápida y mucho más acertadas, pero el proyecto se trataba de realizar la lógica de predicción, no de una aplicación para el usuario (o frontend) final.

## PROCESOS REALIZADOS

### 1. AQI_WAKI/API_SCRIPT

    Obtenemos datos y guardamos en formato CSV, 1 archivo por cada franja horaria (Mañana, Mediodia, Tarde y Noche)
Notebooks

* [api_script](./1.%20api_waqi/api_script.ipynb)

### 2. PREPROCESSING/1r_preprocessing

    Pasamos a limpio los CSV crudos. Eliminamos datos que no están en SPAIN, ponemos bien la hora entre otros.
Notebooks

* [1r_preprocessing](./2.%20preprocessing/1r_preprocessing.ipynb)

#### 2.3 CSV_UNIQUE/join_csv

    Unificamos todos los CSV con el 1r preprocesamiento y se unifican en 1 solo.
Notebooks

* [join_csv](./2.3%20csv_unique/join_csv.ipynb)

### 3 EDA/eda

    "Paja" Miramos que son los datos (pqe nos obligan...)
Notebooks

* [eda](./3.%20EDA_Exploratory_Data_Analysis/eda.ipynb)

### 4 PREPROCESSING_PREVIO_ML/2o_preprocessing

    Aqui limpiamos las filas, haciendo Encoding de las columnas Categoricas, Standarizamos valores, imputamos NaNs, y guardamos todo este preprocessing para usarlo al final con new Data 2 predict
Notebooks

* [2o_preprocessing](./4.%20preprocessing_previo_ml/2o_preprocessing.ipynb)

### 5 MODELO_ML

    1.- Probamos en bruto 10 modelos distintos, tanto de Class como de Reg, para ver cuales son los 2 que mejor funcionan

    2.- Esos 2 que mejor funcionan, tanto de Class como de Reg, les pasamos un GridSearchCV para ver los mejores params.

    3.- Con los params ya definidos y viendo cual es el que mejor funciona, entrenamos los dos modelos finales y guardamos.
Notebooks

* [1. models_selecction](./5.%20Modelo_ML/1.%20models_selecction.ipynb)
* [2. 2_best_model](./5.%20Modelo_ML/2.%202_best_model.ipynb)
* [3. final_models_train](./5.%20Modelo_ML/3.%20final_models_train.ipynb)

![alt 1st](<./images/Screenshot from 2024-07-05 20-38-27.png>)


![alt 2nd](<./images/Screenshot from 2024-07-05 20-38-44.png>)


![image 3rd](<./images/Screenshot from 2024-07-05 20-39-03.png>)


![image 4th](<./images/Screenshot from 2024-07-05 20-39-12.png>)
 

#### 5.2 MODELO_VALIDACION

    Ejecutamos EL MISMO preprocesamiento de los datos con los que entrenamos el modelo, a los nuevos datos.
Notebooks

* [prepro_new_data](./5.2%20Modelo_Validacion/prepro_new_data.ipynb)

![img 5th](<./images/Screenshot from 2024-07-05 20-40-03.png>)