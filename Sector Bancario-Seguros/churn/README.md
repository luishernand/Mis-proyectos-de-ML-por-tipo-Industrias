# Churn for Bank Customers  
<img src="https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/Churn-Rate-Equation.jpg" heiht= 600 width= 550 alt=" ">  

**El Churn Rate** o **Tasa de Cancelación de clientes** es una métrica que mide el número de clientes y suscriptores que han dejado de seguir a una compañía (o han comenzado a seguirla) en un largo período de tiempo.  

## Planteamiento  
La deserción de clientes (también conocida como pérdida de clientes) es uno de los mayores gastos de cualquier organización. Si pudiéramos averiguar por qué un cliente se va y cuándo se va con una precisión razonable, ayudaría enormemente a la organización a diseñar estrategias de múltiples iniciativas de retención. Utilicemos un conjunto de datos de transacciones de clientes de Kaggle para comprender los pasos clave involucrados en la predicción de la deserción de clientes en Python.  

El aprendizaje automático supervisado no es más que aprender una función que asigna una entrada a una salida basándose en pares de entrada y salida de ejemplo. Un algoritmo de aprendizaje automático supervisado analiza los datos de entrenamiento y produce una función inferida, que puede usarse para mapear nuevos ejemplos. Dado que tenemos datos sobre transacciones de clientes actuales y anteriores en el conjunto de datos de una Institución Bancaria, este es un problema de clasificación supervisada estandarizada que intenta predecir un resultado binario (Y / N). 

Como sabemos, es mucho más caro iniciar sesión en un nuevo cliente que mantener uno existente. Es ventajoso para los bancos saber qué lleva a un cliente a la decisión de dejar la empresa. La prevención de abandonos permite a las empresas desarrollar programas de fidelización y campañas de retención para mantener tantos clientes como sea posible.  

**Contenido:**  
- [Planteamiento](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/tree/main/Sector%20Bancario-Seguros/churn#planteamiento)
- [Conjunto de Datos](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/tree/main/Sector%20Bancario-Seguros/churn#conjunto-de-datos)
- [Exploratory Analysis-EDA](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/tree/main/Sector%20Bancario-Seguros/churn#exploratory-data-analysis--eda)
- [modelo](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/README.md#modelo)  
- [Conclusión](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/README.md#conclusi%C3%B3n)
- [Notebook](https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/README.md#notebook)  


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
 
      
**Comentario:**    

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

	NumOfProducts	Exited	size
		1	  0	3675
		1	  1	1409
		2	  0	4242
		2	  1	 348
		3	  0	  46
		3	  1	 220
		4	  1	 60

**Comentario:**    
Clientes que Dejaron de ser nuestros por Cantidad de Productos:  
- Con 1 = 1,409
- Con 2 = 348
- Con 3 = 220
- Con 4 = 60  

**Tenure:**  
![C18] ![c19]   
![c17]



**Comentario:**  
- Clientes con 10 años en el banco representa el 5%
- El mayor abandono se presenta a 1, 3, 5 y 9 años.  



**Distribución de los datos Numericos**    
![c9]  

**Correlación**    
![c10]  

**Outliers**  
![c11]  ![c12]    

**Comentario:**  
- El dataset presenta outliers
- tenemos dos clientes con 92 años poseen saldos
No vamos a eliminar los outliers ya que todavía son clientes nuestros y presentan Balance.  

## Modelo  

Es muy frecuente encontrarnos con datasets con clases desbalanceadas, aplicamos la estrategía de SMOTE  para solucionar esta problemática ya que nuestro conjunto de datos cuenta con pocios registros.Para este conjunto de datos utilizamos las técnica de OverSampling ya que nuestras varaible de salidad(target) presente desbalance en las clases. 
0= 79.63% 1= 20.73%

**SMOTE(OverSampling):** se utiliza para genrear datos sintéticos, utiliza un vecino más cercano para generar datos nuevos. 

Utilizamos la libreria  
```python  
from imblearn.over_sampling import SMOTE
```  
Llevando a nuestra targe o class: 0= 7963, 1 = 7963  

**Modelos Aplicados:**    
- Stacking Model

**Stacking Models:** Utiliza un algoritmo de meta aprendizaje para aprender cómo combinar mejor las predicciones de dos o más algoritmos básicos de Machine Learning. El beneficio del apilamiento es que puede aprovechar las capacidades de una variedad de modelos de buen desempeño en una tarea de clasificación o regresión y hacer predicciones que tienen un mejor desempeño que cualquier modelo individual en el conjunto.
para realizar el stacking utilizamos los siguientes 5 modelos de clasificación:

- KNeighborsClassifier.
- SVC
- DecisionTreeClassifier
- RandomForestClassifier
- MLPClassifier  

**Evaluación**    

Classification Report:

		  precision    recall   f1-score   support

     Cliente        0.87      	0.86      0.87      2426
    Abandono        0.86      	0.87      0.87      2352

    accuracy                          	  0.87      4778
    macro avg       0.87      	0.87      0.87      4778
    weighted avg    0.87      	0.87      0.87      4778  
  

Confussion Matrix:  

![m1]

## Conclusión  
Pudimos Observar que existen diversos factores que pueden afectar la perdida del cliente, entre estos hay factores que no estan estipulados en este conjunto de datos como son: Cantidad de reclamación del cliente, cantidad de veces que el cliente es conctactado por nuestro personal, Tipo de contacto o servicio generado, entre otros.  

Debemos de tener en cuenta la estrategía para tratar la problematica del desbalance de las clases ya que de no balancer los datos o utilizar una estrategía de clase de peso, podría afectar el performace del o los modelo aplicados.  

## Notebook  

1. [EDA and data cleaning](https://nbviewer.jupyter.org/github/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/churn.ipynb)
2. [Modelo de Machine Learning](https://nbviewer.jupyter.org/github/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/Model.ipynb)  

También puede visitar la carpeta [Analisis-EDA-predicciones](https://github.com/luishernand/Analisis-EDA-predicciones) y ver otros notebook :  [churn_rate](https://nbviewer.jupyter.org/github/luishernand/Analisis-_EDA_predictions/blob/master/Churn_rate.ipynb) para una cell-co entre otros.

	
	Creado por:  Luis Hernández   email:   luishernand11@gmail.com





 













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
[c15]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c15.png
[c16]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c16.png
[c17]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c17.png
[c18]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c18.png
[c19]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/c19.png
[m1]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/m1.png
[m2]:https://github.com/luishernand/Mis-proyectos-de-ML-por-tipo-Industrias/blob/main/Sector%20Bancario-Seguros/churn/imagen/m2.png
