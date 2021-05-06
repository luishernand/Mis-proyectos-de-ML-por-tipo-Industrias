# Churn for Bank Customers  
<img src="https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/Churn-Rate-Equation.jpg" heiht= 600 width= 550 alt=" ">  

**El Churn Rate** o **Tasa de Cancelación de clientes** es una métrica que mide el número de clientes y suscriptores que han dejado de seguir a una compañía (o han comenzado a seguirla) en un largo período de tiempo.  

## Planteamiento  
La deserción de clientes (también conocida como pérdida de clientes) es uno de los mayores gastos de cualquier organización. Si pudiéramos averiguar por qué un cliente se va y cuándo se va con una precisión razonable, ayudaría enormemente a la organización a diseñar estrategias de múltiples iniciativas de retención. Utilicemos un conjunto de datos de transacciones de clientes de Kaggle para comprender los pasos clave involucrados en la predicción de la deserción de clientes en Python.  

El aprendizaje automático supervisado no es más que aprender una función que asigna una entrada a una salida basándose en pares de entrada y salida de ejemplo. Un algoritmo de aprendizaje automático supervisado analiza los datos de entrenamiento y produce una función inferida, que puede usarse para mapear nuevos ejemplos. Dado que tenemos datos sobre transacciones de clientes actuales y anteriores en el conjunto de datos de una Institución Bancaria, este es un problema de clasificación supervisada estandarizada que intenta predecir un resultado binario (Y / N). 

Como sabemos, es mucho más caro iniciar sesión en un nuevo cliente que mantener uno existente. Es ventajoso para los bancos saber qué lleva a un cliente a la decisión de dejar la empresa. La prevención de abandonos permite a las empresas desarrollar programas de fidelización y campañas de retención para mantener tantos clientes como sea posible.  

## Conjunto de Datos 
para este proyecto utilizamos  los datos de [kaggle](https://www.kaggle.com/mathchi/churn-for-bank-customers),

   |CustomerId|	Surname | CreditScore|Geography|Gender	|Age	|Tenure  |Balance	|NumOfProducts|HasCrCard|IsActiveMember|EstimatedSalary|Exited|
   |----------|----------|-----------|----------|------- |----|---------|------- |-------------|---------|--------------|-----------------|--------|
 |15634602  |Hargrave    |	 619      |	  France|	Female|	42|	2     |	  0.00|      1	      |     1	|   1	        |    101348.88	|   1|
 |15647311	|Hill	      |     608    |	  Spain	|  Female|	41|	1     |83807.86|      1	      |     0	|      1	 |           112542.58|	   0|
 |15619304	|Onio	      |      502   |	  France	|Female  |	42|	8     |159660.80|     3	      |     1	 |  0	    |        113931.57	|   1|
|15701354	|Boni	      |      699   |	  France	|Female  |	39|	1     |	   0.00|      2	   |     0	 |  0	    |        93826.63	|   0|
 |15737888|	Mitchell	   |     850    |	  Spain	|  Female|	43|	2     | 125510.82|   1	      |     1	 |    1	 |           79084.10	|   0|  


Este dataset consta de **10,000** observaciones y **13** características.  
Descripción:  
- RowNumber—corresponds to the record (row) number and has no effect on the output.
- CustomerId—contains random values and has no effect on customer leaving the bank.
- Surname—the surname of a customer has no impact on their decision to leave the bank.
- CreditScore—can have an effect on customer churn, since a customer with a higher credit score is less likely to leave the bank.
- Geography—a customer’s location can affect their decision to leave the bank.
- Gender—it’s interesting to explore whether gender plays a role in a customer leaving the bank.
- Age—this is certainly relevant, since older customers are less likely to leave their bank than younger ones.
- Tenure—refers to the number of years that the customer has been a client of the bank. Normally, older clients are more loyal and less likely to leave a bank.
- Balance—also a very good indicator of customer churn, as people with a higher balance in their accounts are less likely to leave the bank compared to those with lower balances.
- NumOfProducts—refers to the number of products that a customer has purchased through the bank.
- HasCrCard—denotes whether or not a customer has a credit card. This column is also relevant, since people with a credit card are less likely to leave the bank.
- IsActiveMember—active customers are less likely to leave the bank.
- EstimatedSalary—as with balance, people with lower salaries are more likely to leave the bank compared to those with higher salaries.
- Exited—whether or not the customer left the bank.  

## Exploratory Data Analysis- EDA  

**Excited Variable A predecir(Target):**

![c4]  

**Comentario:**  
- 0= 79.63% 1= 20.73%
- Los datos de salidas están desbalanceados por lo que se debe de aplicar métodos para el balanceo de las clases  

### Features Analytics  

**Gender:**  

  |Geography	| Gender	| count|
  |------------|--------|------|
 |   France	| Male	 |   2753|
 |   France	| Female	 |2261|
 |   Spain	|    Male|	    1388|
 |   Germany|	 Male	 |   1316|
 |   Germany|	 Female	| 1193|
 |   Spain	|    Female	| 1089 | 
 
 ![c1] ![c2] ![c3] ![c5] ![c6] ![c7] ![c8]   
 
      
**Comentario:  

- El 54.57% de los registros presentados en la variable Gender está compuestos por Hombres(Male)
- Francia tiene mayor porcentaje con el 50.14%.  
- El 25% de nuestros clientes salientes son mujeres
- El páis con mayor salida de los clientes es Germany  



**Balance:**  
La cantidad de Nuestos clientes con balance 0 es de 3,117, 500 clientes abandonaron con balance en 0 y 592 que dejaron de ser nuestros clientes que tenían balance Altos. 

**CreditScore:**  
![c13] ![c14]  

      IsActiveMember	HasCrCard	Balance
      	0	           0	          87
      	0	           1	         233
      	1	           0	          65
      	1	           1	         115   
         
  
**Comentario:**  

- Hay 500 personas que abandonaron con creditos por encima de la media.
- 137 Abandono de clientes y Tienen Balance en sus cuentas con el estatus de IsActiveMember.
- 257 Abandono de clientes con Balance y tienen Tarjeta.
- De 115 clientes con estatus activo y con tarjeta, tenemos:
  + 82 Clientes que Abandonaron con Balance por encima de 0.  
  

**HasCrCard:**  
![c15]  

      HasCrCard	Exited	size
	      0	         0	   2332
	      0	         1	    613
	      1	         0	   5631
	      1	         1	   1424  
         
**Comentario:**

- 613 Clientes que han Abandonado que no tenían tarjetas.
- 1,424 clientes que presentaron abandono que tenían tarjetas.  


**NumOfProducts:**  

![c16]  






         


 












[c1]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c1.png
[c2]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c2.png
[c3]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c3.png
[c4]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c4.png
[c5]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c5.png
[c6]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c6.png
[c7]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c7.png
[c8]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c8.png
[c9]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c9.png
[c10]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c10.png
[c11]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c11.png
[c12]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c12.png
[c13]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c13.png
[c14]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c14.png
[c16]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c16.png
[c17]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c17.png
[c18]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c18.png
[c19]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c19.png
[m1]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/m1.png
[m2]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/m2.png
