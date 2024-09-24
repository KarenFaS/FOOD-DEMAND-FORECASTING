# FOOD-DEMAND-FORECASTING

![Image Alt Text](https://www.sas.com/en_gb/resource-center/demand-forecasting/_jcr_content/par/styledcontainer_b10a/image.img.jpg/1500904553463.jpg)

**Importancia del proyecto**\
 El proyecto de predicción de la demanda representa una iniciativa estratégica de gran valor para la empresa de reparto de comidas. La implementación del proyecto permitirá reducir el desperdicio de alimentos, mejorar la satisfacción del cliente y optimizar la cadena de suministro, generando un impacto positivo en la rentabilidad y sostenibilidad del negocio.

**Hipótesis**\
 Un modelo de aprendizaje automático puede identificar patrones en los datos históricos de los clientes y predecir futuras necesidades de compra con mayor precisión que los analistas humanos.

**Fuente de los datos**\
https://datahack.analyticsvidhya.com/contest/genpact-machine-learning-hackathon-1/#ProblemStatement\

**Datasets utilizados**

* train.csv (456548, 9)

* fulfilment_center_info.csv (77, 5)

* meal_info.csv (51 , 3)

***
**CONTENIDO DEL REPOSITORIO**
* Data
* Notebooks con el codigo
* Mejores modelos (a excepción del CATBOOST que es muy pesado)
* Presentación PowerPoint sobre el proyecto
* Memoria del proyecto
* Documento PowerBI con visualización final de las proyecciones

***
**DESCRIPCIÓN DE LOS DATASETS**

>*train.csv*

| Variable  | Definition |
| ------------- | ------------- |
| id 	| Unique ID |
| week 	| Week No |
| center_id | Unique ID for fulfillment center |
| meal_id | Unique ID for Meal |
| checkout_price | Final price including discount, taxes & delivery charges |
| base_price | Base price of the meal |
| emailer_for_promotion | Emailer sent for promotion of meal |
| homepage_featured | Meal featured at homepage |
| num_orders | (Target) Orders Count |

.

>*fulfilment_center_info.csv*

| Variable  | Definition |
| ------------- | ------------- |
| center_id |	Unique ID for fulfillment center |
| city_code |	Unique code for city |
| region_code |	Unique code for region |
| center_type |	Anonymized center type |
| op_area |	Area of operation (in km^2) |

.

>*meal_info.csv*

| Variable  | Definition |
| ------------- | ------------- |
| meal_id |	Unique ID for the meal |
| category |	Type of meal (beverages/snacks/soups….) |
| cuisine |	Meal cuisine (Indian/Italian/…) |


***
**MODELOS DE MACHINE LEARNING**

**METRICA DE EVALUACIÓN**\
RSME: es la desviación estándar de los valores residuales (errores de predicción). Los valores residuales son una medida de la distancia de los puntos de datos de la línea de regresión; RMSE es una medida de cuál es el nivel de dispersión de estos valores residuales. En otras palabras, le indica el nivel de concentración de los datos en la línea de mejor ajuste.

**PRIMER ENFOQUE DE VARIABLES**\
Se aplican los primeros modelos de predicción de Machine Learning utilizando GridSearchCV para identificar los mejores hiperparametros, obteniendo los siguientes resultados:

| Modelo | Score |
|---|---|
| Gradient Boosting Regressor | 61.3902 |
| LGBMRegressor | 57.0845 |
| XGB | 59.9834 |
| **Random Forest Regressor** | **58.1639** |
| Gradient Boosting Regressor_2 | 66.105 |
| Gradient Boosting sin dummies | 65.3313 |

Una de las desventajas con este enfoque y estos modelos es que las proyecciones presentan algunas valores negativos. Para analizar los resultados de estos casos se toman todas las predicciones con valores absolutos.\

**SEGUNDO ENFOQUE DE VARIABLES**\
Para mejorar el score de RSME, se opta por el modelo de CATBOOST que funciona mas eficientemente con variables categoricas, es por ello que se categorizan todas las variables con formato binario. Se escalan las variables numericas con valores mas altos y se transforma logartimicamente el target para evitar predicciones con valores negativos. El resultado: 

| Modelo | Score |
|---|---|
| CATBOOST | 51.7835 |

**DASHBOARD**\

![dashboard](images/PoweBi%20Presentacion%20de%20proyecciones.gif)
