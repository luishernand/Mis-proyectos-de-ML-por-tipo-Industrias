# Credit card Fraud Detection 

![logo] 

## Plantamiento
Cada año, se pierden miles de millones de dinero debido al fraude con tarjetas de crédito, lo que causa grandes pérdidas para los usuarios y la industria financiera. Este tipo de actividad ilícita es quizás la más común y la que causa más preocupaciones en el mundo financiero. En los últimos años se ha prestado gran atención a la búsqueda de técnicas para evitar esta pérdida significativa de dinero. En este proyecto  abordamos el fraude con tarjetas de crédito mediante el uso de un conjunto de datos desbalanceado que contiene transacciones realizadas por usuarios de tarjetas de crédito. Clasifica las transacciones en dos clases: normal y fraudulentas, y está construido con técnicas de inteligencia artificial(Machine Learning y Deep Learning)  

## Conjunto de Datos   
Los datos fueron obtenidos desde: https://www.kaggle.com/mlg-ulb/creditcardfraud  
El conjunto de datos contiene transacciones realizadas con tarjetas de crédito en septiembre de 2013 por titulares de tarjetas europeos.
Las variables de entrada son  numéricas,  que son el resultado de una transformación PCA. Desafortunadamente, debido a problemas de confidencialidad, no podemos proporcionar las características originales y más información de fondo sobre los datos. Las características V1, V2,… V28 son los componentes principales obtenidos con PCA, las únicas características que no se han transformado con PCA son 'Time' y 'Amount'.

composión de los datos: **284,807** registros y **31** características o variables.
|variables|Descripción|
|---------|-----------|
|Time|los segundos transcurridos entre cada transacción y la primera transacción en el conjunto de datos|
|Amount|el Importe de la transacción|
|V1....V28|Variables de entrada numéricas|  


**Target es Class:** es la variable de respuesta y toma el valor 1 en caso de fraude y 0 en caso contrario.  

## Análisis de datos Exploratorio(EDA)  
**Target** o la variable de destino contiene 0(Transacciones Normales)= 28,4315 y 1(Fraudes) = 492, esto representa un 99.83% las transacciones de tipo 0 y el 0.17% para las transaciones de tipo 1. *Este conjunto de datos está muy desequilibrado, ya que  la clase 1(fraudes) representa el 0.17% de todas las transacciones*.  
![class]  

![history]  
![displot]
![box plot]  
  

Podemos Observar los importes que van desde 0 hasta por encima de los 25,000 mil Dolares.  Las trasnsaciones de tipo fraudulentas tienen un menor monto que las normales. 
Para las transaciones de tipo normal berificamos que los montos mayores van desde los 5,026.26 hasta los 25,691.16 estos solo se fectuaron una solo vez.

**Análisis de las transaciones de tipo fraude**  
![trans fraud]  

Como podemos observar en el Gráfico,  transaciones de fraude tienen la particularidad de tener importe desde  0 hasta 252 siendo montos minimos pero efectuados con una cantidad de veces mayor.  

## Modelos Aplicados:
1. Logistic Regression
2. Stacking Models
3. Convulational Neural Net

1. **Logistic Regression:** Aplicamos varios tipos de tecnicas que van desde:
    - Regression Logistica Normal.
   - Logistic Regression with balanced class weigths
   - Logistic  Regression with class weigths
   - Logistic regression SMOTE.
   - Logistic Regression Udernsampling  


**Regression Logistica Normal**  
Aplicamos el modelo de Ml normal sin aplicar ninguna técnica para los tipos de datos desbalanceados. 
El Performace fue:  

                 precision    recall  f1-score   support

      normal       1.00      1.00      1.00     99507
     fraudes       0.82      0.60      0.69       176

    accuracy                           1.00     99683
    macro avg      0.91      0.80      0.85     99683
    weighted avg   1.00      1.00      1.00     99683  
    
  Podemos Observar que tiene una muy buena precision pero no posee buen recal de la clase de fraudes.  
  
 **Logistic Regression with balanced class weigths:** es una  estrategia de penalización para compensar los datos desbalanceados. Utilizaremos un parámetro adicional en el modelo de Regresión logística en donde indicamos weight = “balanced” y con esto el algoritmo se encargará de equilibrar a la clase minoritaria durante el entrenamiento. Veamos:  
 ``` python 
 LogisticRegression(C = 1e5, max_iter=500, class_weight='balanced')
 ```
el performce fue: 
                
                precision    recall  f1-score   support

      normal       1.00      0.97      0.99     99507
     fraudes       0.05      0.89      0.10       176

    accuracy                           0.97     99683
    macro avg      0.53      0.93      0.54     99683
    weighted avg   1.00      0.97      0.98     99683  
    
  Su precicion para la clase de Fraudes fue muy bajo,  su recall Aumneto al 89% 
  
  **Logistic Regression with class weigths**:  utilizamos un peso para la compensar la clase desbalanceada. 
  para esto dividimos la cantidad de la clase 0 enre la clase 1. ejemplo:
  284315/492 = 57.55.
  
  ```python
  class_weigth = {1:57.55}
  LogisticRegression(C = 1e5, max_iter=500, class_weight=class_weigth)
  ```  
  
  en cunato a score nos arrojo:  
                  
                precision    recall  f1-score   support

      normal       1.00      0.99      1.00     99507
     fraudes       0.17      0.83      0.28       176

    accuracy                           0.99     99683
    macro avg      0.58      0.91      0.64     99683
    weighted avg   1.00      0.99      0.99     99683  
    
    Obtuvo comparado con el anterior obtuvo un ligero incremeto en la precision y el f1, pero sigue siendo muy bajos.    
    
  **Logistic regression SMOTE(OverSampling):**  se utiliza para genrear datos sintéticos, utiliza un vecino más cercano para generar datos nuevos.
  
  Nuestra clase ahora tiene los siguientes valores:  
  0 = 284,315
  1 = 284,315  
  
                  precision    recall  f1-score   support

        normal       0.97      0.99      0.98     99316
       fraudes       0.99      0.97      0.98     99705

      accuracy                           0.98    199021
     macro avg       0.98      0.98      0.98    199021
    weighted avg     0.98      0.98      0.98    199021  
    
    
 Con esta estrategia de logramos balancear las clases y lograr un mejor performace general del modelo, su desventaja consite en que pude estasn:
 - Nos aumenta la data.
 - Incremeta el tiempo de entrenamiento
 - podemos alterar la distribución “natural” de esa clase y confundir al modelo en su clasificación  

**Logistic Regression Udernsampling:** elimina las  muestras de la clase mayoritaria para reducirlo e intentar equilibrar la situación. Tiene como “peligroso” o desventaja que podemos prescindir de muestras importantes, que brindan información y por lo tanto empeorar el modelo. Entonces para seleccionar qué muestras eliminar, deberíamos seguir algún criterio.  


0 = 492  
1 = 492  

  
                precision    recall  f1-score   support

      normal       0.92      0.99      0.96       129
     fraudes       0.99      0.91      0.95       117

    accuracy                           0.95       246
    macro avg      0.96      0.95      0.95       246
    weighted avg   0.95      0.95      0.95       246
    
  
  sus resultados son muy buenos de 95% de accuracy, muy buen recall y presicion, comparandolo con la esrategia de Oversampling esta tiene la ventaja en cuanto al tiempo de entrenamiento.  


2. Stacking Models:  Utiliza un algoritmo de meta aprendizaje para aprender cómo combinar mejor las predicciones de dos o más algoritmos básicos de Machine Learning. El beneficio del apilamiento es que puede aprovechar las capacidades de una variedad de modelos de buen desempeño en una tarea de clasificación o regresión y hacer predicciones que tienen un mejor desempeño que cualquier modelo individual en el conjunto.  

para realizar el stacking utilizamos los siguientes 5 modelos de clasificación:  
- KNeighborsClassifier.
- SVC
- DecisionTreeClassifier
- RandomForestClassifier 
- MLPClassifier 

* Evaluación Stacking:  

  |Modelos  |acc	| mcc	|f1|
  |-----|-----|---------|---|  
  |rf	|0.959391	|0.919522	|0.958333|  
  |stack	|0.959391	|0.918961	|0.958763|  
  |dt	|0.928934	|0.857864	|0.928571|  
  |mlp	|0.908629	|0.828120	|0.900000|  
  |knn	|0.680203	|0.360375	|0.676923|  
  |svc	|0.517766	|0.124987	|0.059406|  

  
            
                  precision    recall  f1-score   support

        normal       0.95      0.97      0.96        99
         fraudes     0.97      0.95      0.96        98

        accuracy                         0.96       197
        macro avg    0.96      0.96      0.96       197
        eighted avg  0.96      0.96      0.96       197
        
   El performace de es muy bueno de un 96% y muy buen recall
   
     
**Confussion Matrix:**  

![lr]  ![balanced] ![weigth] ![smote] ![undersampling]  ![stack]  

Podemos obeservar que la combinación de varios modelos nos un mejor resultado.  

3. Convulational Neural Net: 
 
Model: sequential

|Layer (type)|                 Output Shape|              Param |   
|------------|-----------------------------|--------------------|
  |conv1d (Conv1D)|              (None, 29, 32)|            96  |      

  |batch_normalization| (BatchNo (None, 29, 32) |           128|       

  |dropout (Dropout)  |          (None, 29, 32) |           0|         

  |conv1d_1 (Conv1D) |           (None, 28, 64) |           4160|      

  |batch_normalization_1 |(Batch (None, 28, 64)  |          256|       

  |dropout_1 (Dropout)  |        (None, 28, 64) |           0  |       

  |flatten (Flatten)            (None, 1792)|              0  |       

  |dense (Dense)   |             (None, 64)                114752 |   

  |dropout_2 (Dropout)  |        (None, 64)                0 |        

  |dense_1 (Dense)  |            (None, 1) |                65 |       

Total params: 119,457
Trainable params: 119,265
Non-trainable params: 192  



  

  




[box plot]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/boxplot_amount.png

[class]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/clase_value_counts.png

[displot]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/displot%20amount.png


[history]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/distribucion%20monto%20clase.png

[elbow]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/elbow%20method.png

[logo]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/logo.png


[trans fraud]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/montos%20transaciones%20fraudeluentas.png


[balanced]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/lr%20balanced.png

[undersampling]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/lr%20undersampling.png 

[lr]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/lr.png  

[smote]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/lr_smote.png  

[weigth]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/class%20weigth.png  

[stack]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/mtx_stack.png
