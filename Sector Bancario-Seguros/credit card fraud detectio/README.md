# Credit card Fraud Detection 

![logo] 

## Plantamiento
Cada año, se pierden miles de millones de dinero debido al fraude con tarjetas de crédito, lo que causa grandes pérdidas para los usuarios y la industria financiera. Este tipo de actividad ilícita es quizás la más común y la que causa más preocupaciones en el mundo financiero. En los últimos años se ha prestado gran atención a la búsqueda de técnicas para evitar esta pérdida significativa de dinero. En este proyecto  abordamos el fraude con tarjetas de crédito mediante el uso de un conjunto de datos desbalanceado que contiene transacciones realizadas por usuarios de tarjetas de crédito. Clasifica las transacciones en dos clases: normal y fraudulentas, y está construido con técnicas de inteligencia artificial(Machine Learning y Deep Learning)  

## Conjunto de Datos   
Los datos fueron obtenidos desde: https://www.kaggle.com/mlg-ulb/creditcardfraud  
El conjunto de datos contiene transacciones realizadas con tarjetas de crédito en septiembre de 2013 por titulares de tarjetas europeos.
consta de **284,807** observaciones y **31** características,  solo con variables de entrada numéricas que son el resultado de una transformación PCA. Desafortunadamente, debido a problemas de confidencialidad, no podemos proporcionar las características originales y más información de fondo sobre los datos. Las características V1, V2,… V28 son los componentes principales obtenidos con PCA, las únicas características que no se han transformado con PCA son 'Time' y 'Amount'. .

composión de los datos:
|variables|Descripción|
|---------|-----------|
|Time|los segundos transcurridos entre cada transacción y la primera transacción en el conjunto de datos|
|Amount|el Importe de la transacción|
|Class|es la variable de respuesta y toma el valor 1 en caso de fraude y 0 en caso contrario|
|V1....V28|Variables de entrada numéricas|
 


[box plot]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/boxplot_amount.png

[class]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/clase_value_counts.png

[displot]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/displot%20amount.png


[history]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/distribucion%20monto%20clase.png

[elbow]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/elbow%20method.png

[logo]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/logo.png


[trans fraud]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/credit%20card%20fraud%20detectio/archivos_data_imagen/montos%20transaciones%20fraudeluentas.png


