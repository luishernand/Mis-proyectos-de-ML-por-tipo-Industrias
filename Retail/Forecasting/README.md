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

** Distribución de las variables catégoricas**  
![f1]  

- El tipo de tienda **a** posee la mayor cantidad de registros
- El  surtido(Assortment) de mayor predominio es el básico 
- La temporada de mayor promoción es jan, april, jul, oct  





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
