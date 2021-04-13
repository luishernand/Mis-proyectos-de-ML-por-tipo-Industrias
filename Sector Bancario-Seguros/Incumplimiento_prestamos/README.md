# Loan Default- Incumplumiento de Préstamo  
![img](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/Incumplimiento_prestamos/data/logo.jpg)

**Que es El incumplimiento del préstamo:**  
ocurre cuando un prestatario no paga una deuda de acuerdo con el acuerdo inicial. En el caso de la mayoría de los préstamos al consumo, esto significa que se han perdido pagos sucesivos en el transcurso de semanas o meses. Afortunadamente, los prestamistas y los administradores de préstamos por lo general permiten un período de gracia antes de penalizar al prestatario después de no realizar un pago. El período entre la falta de pago de un préstamo y el incumplimiento del préstamo se conoce como morosidad. El período de morosidad le da al deudor tiempo para evitar el incumplimiento contactando a la entidad administradora de sus préstamos o haciendo los pagos atrasados.


## Planteamiento del problema:

Para clasificar si el prestatario incumplirá el préstamo utilizando  a partir de determinadas características del cliente. Eso significa, dado un conjunto de
nuevas variables predictoras, necesitamos predecir si Si el préstamo fue pagado o esta en proceso de cobro. Para esto utilizaremos Modelos de Clasificación de Machine Learning en python.  

## Conjunto de Datos: 
para este proyecto bajamos los datos de [kaggle](https://www.kaggle.com/), [loan_train.csv](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/Incumplimiento_prestamos/data/loan_train.csv).
El conjunto de datos consta de **346** observaciones y **8** características.

|loan_status|	Principal|	terms|	effective_date|	due_date|	age	|education	Gender|
|-----------|----------|----------|----------|----------|----|----------|
|0|	PAIDOFF|	1000|	30|	2016-09-08|	2016-10-07|	45|	High School or Below	|male|
|1|	PAIDOFF|	1000	|30|	2016-09-08|	2016-10-07|	33|	Bechalor	|female|
|2|	PAIDOFF|	1000|	15|	2016-09-08|	2016-09-22|	27|	college	|male|
|3|	PAIDOFF|	1000	|30|	2016-09-09	|2016-10-08|	28	|college	|female|
|4|	PAIDOFF|	1000	|30|	2016-09-09	|2016-10-08|	29|	college	|male|

 
## Data Engineering-(Ingeniería de datos):  
No tenía características vacías e irrelevantes.  
+ Los valores de cadena se han formateado a números enteros.
+ Los valores categóricos se han transformado en numéricos.
+ Se han creado variables para agregarle valor.
+ Se han eliminado las variables redundantes.

**Predictor Variables-(Variables Predcitorias)**:
A continuación se mencionan las características utilizadas para nuestro modelo:  
|Field	|Description|Descripcón|
|-------|-----------|----------|
|Principal|Basic principal loan amount at the|Monto Básico del préstamo|
|Terms|	Origination terms which can be weekly (7 days), biweekly, and monthly payoff schedule|Plazos de originación que pueden ser semanales (7 días), quincenales y programas de pago mensuales|
|Effective_date|	When the loan got originated and took effects|Cuándo se originó y entró en vigor el préstamo|
|Due_date|	Since it’s one-time payoff schedule, each loan has one single due date|Dado que se trata de un calendario de liquidación único, cada préstamo tiene una única fecha de vencimiento|
|Age|	Age of applicant|Edad de la solicitante|
|Education|	Education of applicant|Educacion del solicitante|
|Gender|	The gender of applican|Genero|


**Target Variable-(Destino o a predecir)** 
La variable de destino en nuestro conjunto de datos es Loan_status	que muestra el estado del préstamo. Tiene 2 diferentes datos:
PAIDOFF y COLLECTION 

## Analisis de Datos (EDA):

La variable de destino o Target cuenta con la siguiente cantidad de registros:
PAIDOFF =260, COLLECTION =86
![a1](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/Incumplimiento_prestamos/data/target_value_counts.png)  
Estos datos nos indican que el 75.14% de las persanas ya han pagado su prestamos, el resto se encuentra en morosidad.


![a2](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/Incumplimiento_prestamos/data/prestamo-genero.png)
|Gender|PAIDOFF|COLLECTION|
|------|-------|----------|
|female | 86.54% |     13.46%|    
|male   |  73.13% |   26.87%|  
  
  
Day of week: 
Notamos  que las personas que obtienen el préstamo al final de la semana no lo cancelan, así que usamos la binarización de funciones para establecer valores de umbral inferiores al día 4.  
![a3](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/Incumplimiento_prestamos/data/day_ofweek.png)

Educación de los prestatarios:  
![ed] ![nivel]
1. High School or Below con 151.
2. college con 149.
3. Bechalor con 44.
4. Master or Above con 2          



## Modelos Aplicados  
1. KNeighborsClassifier
2. DecisionTreeClassifier
3. Support Vector Machine
4. Logistic Regression  

[ed]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/Incumplimiento_prestamos/data/educacion.png
[nivel]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/Incumplimiento_prestamos/data/Nivel%20de%20Educaci%C3%B3n_texto.png
