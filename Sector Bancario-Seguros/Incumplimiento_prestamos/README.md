# Loan Default- Incumplumiento de Préstamo  
![img](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/Incumplimiento_prestamos/data/logo.jpg)

**Que es El incumplimiento del préstamo:**  
ocurre cuando un prestatario no paga una deuda de acuerdo con el acuerdo inicial. En el caso de la mayoría de los préstamos al consumo, esto significa que se han perdido pagos sucesivos en el transcurso de semanas o meses. Afortunadamente, los prestamistas y los administradores de préstamos por lo general permiten un período de gracia antes de penalizar al prestatario después de no realizar un pago. El período entre la falta de pago de un préstamo y el incumplimiento del préstamo se conoce como morosidad. El período de morosidad le da al deudor tiempo para evitar el incumplimiento contactando a la entidad administradora de sus préstamos o haciendo los pagos atrasados.


## Planteamiento del problema:

Para clasificar si el prestatario incumplirá el préstamo utilizando  a partir de determinadas características del cliente. Eso significa, dado un conjunto de
nuevas variables predictoras, necesitamos predecir si Si el préstamo fue pagado o esta en proceso de cobro. Para esto utilizaremos Modelos de Clasificación de Machine Learning en python.  

 
## Data Engineering:  
El conjunto de datos consta de **346** observaciones y **8** características, no tenía características vacías e irrelevantes.  
+ Los valores de cadena se han formateado a números enteros.
+ Los valores categóricos se han transformado en numéricos.
+ Se han creado variables para agregarle valor.
+ Se han eliminado las variables redundantes.

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


|Loan_status|	Whether a loan is paid off on in collection| Si el prestamo fue pagado o esta en proceso de cobro|
