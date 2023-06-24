# Diamonds Prediction Project
Machine Learning Project based in the price prediction for a diamond's dataset

# Contexto
El proyecto consiste en crear modelo de predicción para calcular el precio de un listado de diamantes dónde tenemos el un listado de features pero no sabemos que precio tienen en el mercado. 

# Mi proyecto
Para averigual el precio de los diamantes que tenemos para testear he seguido los siguientes pasos: 

- Data Extraction
- EDA
- Preprocesing
- Training
- Predict
- Result

Se explican los pasos a continuación: 

1. Extraer la data
Tenemos una Base de Datos en un archivo .db de dónde necesitamos extraer los datos para entrenar a mi modelo. Lo extraigo con la libreria duckdb y posteriormente uno cada extracción para crear un dataframe que me incluya toda la información que necesito:

-  price
- carat
- depth
- table
- x
- y
- z
- city
- clarity
- color
- cut 

En este dataset obtengo 40.455 filas de información.

EDA: Hago un análisis para asegurarme de que no tengo datos nulos (no es posible entrenar un modelo con datos nulos ni con datos categóricos)

Guardo en CSV el dataset generado para mi entrenamiento. 

2. Preprocesing

Describo a continuación los pasos que he seguido en "preprocesing"

- Comienzo llamando al CSV que he creado para mi entrenamiento y reviso los datos. 

- Decido eliminar la columna "city" porque en otras pruebas no me ha ayudado a mejorar modelo. 

- Cargo mi dataset de test

- Le aplico la misma lógica que a "training" dónde le elimino la columna "city". Como el dataset de "test" también cuenta con la columna "id", también la elimino para que se queden siendo iguales. 

- Ahora cargo el dataset resultante de mi mejor modelo de entrenamiento. En este dataset tengo un listado resultante de precios estimados. 

- Para mejorar mi modelo, aplico estos precios estimados a mi dataset de test y se lo añado al dataset de trating concatenandolo. 

- Ahora, en vez de entrenar con 40.455 filas, entreno mis datos con 53.940 filas. 

- Divido mi dataset de entrenamiento en 2 separando las columnas categóricas de las numéricas. 

- Trabajo sobre mis datos categóricos, convirtiendolos a numéricos con "one hot encoding". 

- Concateno ambos dataframes obteniendo un único dataframe con datos numéricos. 

## FEATURE ENGINEERING

Creo nuevas features sobre cada uno de los valores categóricos, comparandolos con los quilates: 

- cut/weight_Fair
- cut/weight_Good
- cut/weight_Ideal
- cut/weight_Premium
- cut/weight_Very Good
- color/weight_D
- color/weight_E
- color/weight_F
- color/weight_G
- color/weight_H
- color/weight_I
- color/weight_J
- clarity/weight_I1
- clarity/weight_IF
- clarity/weight_SI1
- clarity/weight_SI2
- clarity/weight_VS1
- clarity/weight_VS2
- clarity/weight_VVS1
- clarity/weight_VVS2

Elimino las features que ya no me interesan que son todas las variables simples de corte, color y clariadad. 

Ahora aplico los mismos pasos sobre mi dataset de test. 

Guardo los 2 datasets: training y test. 

## MODEL TRAINING

Cargo los 2 datasets: training y test.

Guardo en X e Y mis Features y Target:

- X: Las features que mejor me han funcionado son:

carat
depth
table
x
y
z
cut/weight_Fair
cut/weight_Good
cut/weight_Ideal
cut/weight_Premium
cut/weight_Very
color/weight_D
color/weight_E
color/weight_F
color/weight_G
color/weight_H
color/weight_I
color/weight_J
clarity/weight_I1
clarity/weight_IF
clarity/weight_SI1
clarity/weight_SI2
clarity/weight_VS1
clarity/weight_VS2
clarity/weight_VVS1
clarity/weight_VVS2

- Y: Mi target es "precio"

## SCALING

Aplico RobustScaling

## MODELING

El modelo que mejor me ha funcionado es LGBMRegressor


