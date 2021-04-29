# Forecasting para empresas de Reatil
![logo]  

El forecast o pronóstico es la estimación de ventas que tenemos para un determinado periodo de tiempo. Para ello utilizaremos datos históricos, valoraciones del equipo de marketing, información de los profesionales de ventas o cualquier otro indicador disponible para obtener la cifra más real posible.

El forecast puede realizarse desde un punto de vista institucional, en el que la empresa hace sus predicciones sobre la demanda de sus productos para que los distintos departamentos (logística, producción, financiero, etc) tomen en cuenta esta información en su planificación, o desde un punto de vista personal, en el que el profesional de ventas declara lo que venderá en el futuro.

**Objetivo**  
En un mercado tan competitivo y complejo es indispensable conocer de la manera más fiable posible el futuro a corto, medio y largo plazo para realizar una planificación optima e invertir consecuentemente los recursos.

Si utilizamos esta arma correctamente podremos reducir inventarios, disminuir los riesgos de obsolescencia de nuestros productos, mejorar la coordinación entre los distintos procesos del negocio al tener un punto de partida común, reaccionar antes las crisis con mayor antelación y mejorar la atención al cliente.

Esto permitirá que detectemos los problemas con anterioridad por lo que podremos buscar soluciones que atajen los obstáculos antes de que estos causen un impacto mayor.

 

**Funcionamiento**  
Existen múltiples métodos para realizar un forecast dependiendo del tamaño y sector de la empresa. Lo importante es que sea lo más fiable posible ya que es la base sobre la que tomaremos decisiones que afectarán al porvenir de la empresa.

## Plantamiento 
**Rossmann Store Sales**  
Opera más de 3.000 farmacias en 7 países europeos. Actualmente, los gerentes de las tiendas Rossmann tienen la tarea de predecir sus ventas diarias con hasta seis semanas de anticipación. Las ventas en las tiendas están influenciadas por muchos factores, incluidas las promociones, la competencia, las vacaciones escolares y estatales, la estacionalidad y la localidad. Con miles de gerentes individuales que predicen las ventas en función de sus circunstancias únicas, la precisión de los resultados puede variar bastante.  

Objetivo: explorar datos y predecir 6 semanas de ventas diarias para 1115 tiendas ubicadas en Alemania.  
Este cuaderno se centra principalmente en el análisis de series de tiempo, un tema que no se trata en Rossmann Competition Kernels. Luego discutimos las ventajas y los inconvenientes del modelado con Seasonal ARIMA y Prophet.  

Como suele suceder, comenzamos con el Análisis de datos exploratorios de las principales métricas que revelan las tendencias y patrones actuales en los datos, lo que proporciona una base sólida para el análisis causal adicional.  

Además, como alternativa a la previsión con Prophet, utilizamos uno de los algoritmos de aumento de gradiente extremo más robustos y Extreme Gradient Boosting for regression.  

## Conjunto de datos  

Dataset: https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/tree/main/Retail/Forecasting/files/data  

**Descripción**:  
- Id - an Id that represents a (Store, Date) duple within the test set
- Store - a unique Id for each store
- Sales - the turnover for any given day (this is what you are predicting)
- Customers - the number of customers on a given day
- Open - an indicator for whether the store was open: 0 = closed, 1 = open
- StateHoliday - indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all - schools are closed on public holidays - and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None
- SchoolHoliday - indicates if the (Store, Date) was affected by the closure of public schools
- StoreType - differentiates between 4 different store models: a, b, c, d
- Assortment - describes an assortment level: a = basic, b = extra, c = extended
- CompetitionDistance - distance in meters to the nearest competitor store
- CompetitionOpenSince[Month/Year] - gives the approximate year and month of the time the nearest competitor was opened
- Promo - indicates whether a store is running a promo on that day
- Promo2 - Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating
- Promo2Since[Year/Week] - describes the year and calendar week when the store started participating in Promo2
- PromoInterval - describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts - in - February, May, August, November of any given year for that store  

composión de los datos de store.csv: **1115** registros y **10** características o variables, para nuesro train dataset **41088** registros y  **8** variables.  

## Análisis de datos Exploratorio(EDA)  

**1. Distribución de las variables catégoricas**  
![f1]  
- El tipo de tienda **(a)** posee la mayor cantidad de registros.
- El  surtido(Assortment) de mayor predominio es el básico. 
- La temporada de mayor promoción es jan, april, jul, oct. 

**2. Average de ventas por clientes** 
es de **9.49** dolares  

**3. ECDF: función de distribución acumulativa empírica**  
estima la verdadera función de densidad acumulativa subyacente de los puntos en la muestra; Se garantiza virtualmente que converge con la distribución verdadera a medida que el tamaño de la muestra se hace lo suficientemente grande. Análizamos las variables: Sales, Customers y salespercustomers respectivamente.  
![f2]  

**3. Distribución de las Ventas**  
![f3]  
- Hay 172,871 tiendas sin ventas
- comprendido entre '2015-07-29' y '2015-07-31'
- hay 54 tiendas que fueron abiertas sin ventas  

**4. StoreType**  
    
    Stores  Promedio de ventas
     b       10233.380141
     c       6933.126425
     a       6925.697986
     d       6822.300064

                      count	       mean	             std	     min	    25%	     50%	        75%   	  max
    StoreType								
      a	             457042.0  	 6925.697986	  3277.351589	   46.0	  4695.25	  6285.0	   8406.00	   41551.0
      b	              15560.0	  10233.380141	  5155.729868	 1252.0	  6345.75	  9130.0	  13184.25	   38722.0
      c	             112968.0	   6933.126425	  2896.958579	  133.0	  4916.00	  6408.0	   8349.25	   31448.0
      d	             258768.0	   6822.300064	  2556.401455	  538.0	  5050.00	  6395.0	   8123.25	   38037.0

- el tipo de tienda B es la de mayor promedio de ventas
- las ventas minimas de B son mayores que las demas
- el tipo de tienda a optiene ventas maximas de 41,551  

![f4]
![f5]
![f6]
![f7]  

- La tendencia de las ventas con promoción es ascendente
- El mes con mayor tendencia ascendente es diciembre
- Los dias que no participa de promoción de mayor venta son viernes y domingo
- Los lunes cunado hay promoción  

**5. Times Series**  
![8]  
- Las ventas por tipo de tienda a y c alcanzan su punto maximo en temporada navideña.
- En las tiendas de tipo D fuera posible su tope máximo en temporada navideña pero no tenemos datos emtre jul 2014 y enero 2015.  

**6. Autocorrelation**  
El siguiente paso en el análisis de nuestra serie temporal es revisar los gráficos de la función de autocorrelación (ACF) y la función de autocorrelación parcial (PACF).  

ACF es una medida de la correlación entre la serie temporal con una versión retrasada de sí misma. Por ejemplo, en el retraso 5, ACF compararía series en el instante de tiempo "t1" ... "tn" con series en el instante "t1-5" ... "tn-5" (t1-5 y tn son puntos finales).   

PACF, por otro lado, mide la correlación entre las series temporales con una versión rezagada de sí misma, pero después de eliminar las variaciones explicadas por las comparaciones intermedias. P.ej. en el rezago 5, comprobará la correlación pero eliminará los efectos ya explicados por los rezagos 1 a 4.  

![f9]  

Podemos leer estos gráficos horizontalmente. Cada par horizontal es para un 'StoreType', de A a D. En general, esos gráficos muestran la correlación de la serie consigo misma, rezagada por x unidades de tiempo correlación de la serie consigo misma, rezagada por x unidades de tiempo.  

- Hay dos cosas en común para cada par de gráficos: no aleatorias de la serie de tiempo y alto retardo-1 (que probablemente necesitará un orden superior de diferenciación d / D).  
- Tipo A y tipo B: ambos tipos muestran estacionalidades en ciertos rezagos. Para el tipo A, es cada duodécima observación con picos positivos en los retrasos 12 (s) y 24 (2s) y así sucesivamente. Para el tipo B, es una tendencia semanal con picos positivos en los retrasos 7 (s), 14 (2 s), 21 (3 s) y 28 (4 s).  

- Tipo C y tipo D: las parcelas de estos dos tipos son más complejas. Parece que cada observación está correlacionada con sus observaciones adyacentes.  

## Time Series Analysis and Forecasting with Prophet  
![t1]  
- Podemos Observar el que las ventas se incrementan en temporada navideña. 
- Período de los datos 01-01-2013 hasta 31-7-2015.
- Realizaremos un pronóstico de 42 días (11-9-2015). 


![t2]  
Prophet traza los valores observados de nuestra serie de tiempo (los puntos negros), los valores pronosticados (línea azul) y los intervalos de incertidumbre de nuestros pronósticos (las regiones sombreadas en azul).  
![t3]  
La primera gráfica muestra que las ventas mensuales de la tienda número 1 han ido disminuyendo linealmente con el tiempo y la segunda muestra las brechas de vacaciones incluidas en el modelo. El tercer gráfico destaca el hecho de que el volumen semanal de ventas de la semana pasada alcanza su punto máximo hacia el lunes de la semana siguiente, mientras que el cuarto gráfico muestra que la temporada de mayor actividad se produce durante las vacaciones de Navidad.  

  

## Pronóstico con XGBRegressor  

Parámetros: 
```python
XGBRegressor(base_score=0.5, booster='gbtree', colsample_bylevel=1,
             colsample_bynode=1, colsample_bytree=1, gamma=0, gpu_id=-1,
             importance_type='gain', interaction_constraints='',
             learning_rate=0.300000012, max_delta_step=0, max_depth=6,
             min_child_weight=1, missing=nan, monotone_constraints='()',
             n_estimators=100, n_jobs=4, num_parallel_tree=1, random_state=0,
             reg_alpha=0, reg_lambda=1, scale_pos_weight=1, subsample=1,
             tree_method='exact', validate_parameters=1, verbosity=None)
```  

### Evaluación  

R2, el coeficiente de determinación, determina la capacidad de un modelo para predecir futuros resultados. El mejor resultado posible es 1.0, y ocurre cuando la predicción coincide con los valores de la variable objetivo. R2 puede tomar valores negativos pues la predicción puede ser arbitrariamente mala. Cuando la predicción coincide con la esperanza de los valores de la variable objetivo, el resultado de R2 es 0. Se define como 1 menos la suma de cuadrados totales dividido por la suma de cuadrados de los residuos.

**resultado:** 0.9993151904235793

![m1]  


## Conclusión del pronóstico de series de tiempo  
Durante esta parte, discutimos el análisis de series de tiempo con gráficos .seasonal_decompose (), ACF y PCF y ajustamos el modelo de pronóstico utilizando un nuevo procedimiento de Facebook Prophet.  

Ahora podemos presentar las principales ventajas e inconvenientes de la predicción de series de tiempo:  

**Ventajas**
- Potente herramienta para el pronóstico de series de tiempo, ya que tiene en cuenta las dependencias del tiempo, las estaciones y los días festivos (Prophet: manualy).
- Se implementa fácilmente con R auto.arima () del paquete de pronóstico, que ejecuta una búsqueda de cuadrícula compleja y un - algoritmo sofisticado detrás de escena.

**Inconvenientes**  
- No detecta interacciones entre características externas, lo que podría mejorar el poder de pronóstico de un modelo. En nuestro caso, estas variables son Promo y CompetitionOpen.  
- Aunque Prophet ofrece una solución automatizada para ARIMA, esta metodología está en desarrollo y no es completamente estable.
- El ajuste del modelo ARIMA estacional necesita de 4 a 5 temporadas completas en el conjunto de datos, lo que puede ser el mayor inconveniente para las nuevas empresas.
- ARIMA estacional en Python tiene 7 hiperparámetros que solo se pueden ajustar manualmente, lo que afecta significativamente la velocidad del proceso de pronóstico. 


El análisis de series de tiempo es imprescindible para los datos de series de tiempo. Va mucho más profundo que el análisis de datos exploratorios ad-hoc, revelando tendencias, no aleatoriedad de los datos y estacionalidades.

Aunque Prophet esta herramienta aún está en desarrollo, tiene todo configurado para el modelado avanzado, ya que puede dar cuenta de los puntos de cambio en las tendencias y los días festivos en los datos. Mientras tanto, la herramienta más sofisticada para el análisis de series temporales sigue siendo auto.arima del paquete de pronóstico R.  

Se puede lograr un salto significativo en el rendimiento de pronóstico del modelo instalado anteriormente, XGboost con la biblioteca xgboost, aumentando el número y el rango de hiperparámetros. 

Otro método que no cubrí aquí es un modelo de regresión Stacking, que funciona muy bien para conjuntos de datos de tamaño pequeño o mediano. Básicamente, combinaríamos XGboost, RandomForest, NN y SVM para la regresión. Y luego apílelos juntos construyendo el modelo final.  

Con respecto al modelo XGboost, se puede utilizar LightGBM, una biblioteca potencialmente mejor que XGboost.  

## Notebook  

1. [Análisis de datos exploratorio](https://nbviewer.jupyter.org/github/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/notebooks/Forecasts.ipynb)
2. [Modelo Prohet](https://nbviewer.jupyter.org/github/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/notebooks/Times%20Series.ipynb)
3. [Modelo XGboost](https://nbviewer.jupyter.org/github/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/notebooks/model.ipynb) 





[logo]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/ab299b25ce9fe14e778f95b44f7ac322a2fc0e2f/Retail/Forecasting/files/imagenes/logo.jpg
[f1]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f1.png
[f2]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f2.png
[f3]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f3.png
[f4]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f4.png
[f5]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f5.png
[f6]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f6.png
[f7]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f7.png
[f8]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f8.png
[f9]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/f9.png
[t1]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/t1.png
[t2]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/t2.png
[t3]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/t3.png
[m1]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Retail/Forecasting/files/imagenes/m1.png
