# Proyecto_Machine_Learning
Construcción de un modelo de regresión y clasificación.

# Descripción:
Creamos un modelo de regresión para predecir la nota final y un modelo de clasificación para predecir aprobados y suspensos, a partir de unos datos de estudiantes.  
Primero hacemos un EDA (01_EDA.ipynb) para ver qué datos tenemos. En él hacemos una vista previa de los datos, vemos los nulos que hay y si hay inconsistencias (aprobados con notas menores a 60 o suspensos con notas mayores).  

Iniciamos el preprocesamiento (02_Preprocesamiento.ipynb) cargando el archivo con los datos ya analizados. En las columnas categóricas con valores nulos ponemos desconocido y en horas de sueño imputamos con la mediana.  
Creamos una copia para regresión en la cual usamos one_hot_encoder para las columnas nivel_dificultad y tiene_tutor y target_encoding para horario_estudio y estilo_aprendizaje. En target_encoding usamos smoothing para suavizar el impacto de los datos desconocidos, ya que hay pocos. Aplicamos MinMaxScaler para igualar la importancia de los datos. Guardamos el archivo df_regresion.csv.  

Para clasificación hacemos lo mismo que en regresión cambiando la variable objetivo de nota final a aprueba y lo guardamos df_clasificacion.csv.  

Creamos el modelo de regresión lineal (03_Modelo_Regresión.ipynb). Separamos la variable objetivo y quitamos la columna aprobado. Creamos el conjunto de entrenamiento(80%) y el de prueba(20%). Creamos el modelo y lo entrenamos, hacemos las predicciones con el conjunto de prueba y creamos un gráfico para ver los resultados. Vemos que el modelo, en alumnos que tienen notas bajas, es optimista, predice notas más altas. Al contrario que con las notas altas. Graficamos residuos, los errores se ditribuyen de forma aleatoria lo que dice que el modelo no tiene sesgo. Vemos la importancia de cada característica, horas de estudio semanal, nota anterior y tasa de asistencia son las que más importancia tienen. Calculamos las métricas, en ellas podemos ver que no existe sobreajuste y para un modelo simple prediciendo notas de examen un MAE de 6 puede considerarse un éxito. Entrenamos el modelo con todos los datos (entrenamiento y prueba) y guardamos el modelo (modelo_regresion.pkl).  

En el modelo de clasificación vemos que tenemos 900 datos para aprobados y 100 para suspensos. Esto puede ser un problema ya que el modelo podría predecir una mayoría de aprobados y tener una precisión cercana al 90%. Por ello creamos el modelo aplicando class_weight= 'balanced'. En este caso quitamos, aparte de la variable objetivo, la  nota final.  En la matriz de confusión vemos que el modelo predice bien los suspensos (solo se escapan 4) pero hay 50 aprobados que predice suspenso. Al probar sin ajuste de balanceo de clase predice perfectamente los aprobados (solo falla en 1) pero de los 15 suspensos solo detecta 2. Mejor detectar 50 que aprobaran como suspensos que no predecir que todos van a aprobar. Nos quedamos con este modelo. Calculamos las métricas, vemos que son casi iguales para el conjunto de entrenamiento y de prueba por lo que puede considerarse estable. El modelo predice bien el 97% de los aprobados e identifica el 73% de los alumnos que pueden suspender. Con un 0.83 de f1-score se puede decir que es un buen modelo. Vemos qué características son las que más influyen que al igual que en el modelo de regresión son horas de estudio semanal, nota anterior y tasa de asistencia. Entrenamos el modelo con todos los datos y guardamos (modelo_clasificación.pkl)  

# Archivos adjuntos:

- 01_EDA.ipynb
- 02_Preprocesamiento.ipynb
- 03_Modelo_Regresión.ipynb
- 04_Modelo_Clasificacion.ipynb
- dataset_estudiantes.csv (Datos originales)
- df_clasificacion.csv (Datos procesados para el modelo de clasificación)
- df_regresion.csv (Datos procesados para el modelo de regresión)
- modelo_clasificación.pkl (Modelo de clasificación entrenado)
- modelo_regresion.pkl (Modelo de regresión entrenado)

# Autor: 
Antonio Fernández
@antonio28863

