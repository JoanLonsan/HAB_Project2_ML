# PROYECTO 2

## GRUPO A

### 1. AQI_WAKI/API_SCRIPT

    Obtenemos datos y guardamos en formato CSV, 1 CSV por cada franja horaria (Mañana, Mediodia, Tarde y Noche)

### 2. PREPROCESSING/1r_preprocessing

    Pasamos a limpio los CSV crudos. Eliminamos datos que no están en SPAIN, ponemos bien la hora entre otros.

#### 2.3 CSV_UNIQUE/join_csv

    Unificamos todos los CSV con el 1r preprocesamiento y se unifican en 1 solo.

### 3 EDA/eda

    "Paja" Miramos que son los datos (pqe nos obligan...)

### 4 PREPROCESSING_PREVIO_ML/2o_preprocessing

    Aqui limpiamos las filas, haciendo Encoding de las columnas Categoricas, Standarizamos valores, imputamos NaNs, y guardamos todo este preprocessing para usarlo al final con new Data 2 predict

### 5 MODELO_ML

    1.- Probamos en bruto 10 modelos distintos, tanto de Class como de Reg, para ver cuales son los 2 que mejor funcionan

    2.- Esos 2 que mejor funcionan, tanto de Class como de Reg, les pasamos un GridSearchCV para ver los mejores params.

    3.- Con los params ya definidos y viendo cual es el que mejor funciona, entrenamos los dos modelos finales y guardamos.

#### 5.2 MODELO_VALIDACION

    Ejecutamos EL MISMO preprocesamiento de los datos con los que entrenamos el modelo, a los nuevos datos.