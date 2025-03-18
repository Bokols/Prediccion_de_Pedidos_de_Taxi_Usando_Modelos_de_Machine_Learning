# **Predicción de Pedidos de Taxi Usando Modelos de Machine Learning**  

## **Introducción**  
En este proyecto, el objetivo fue desarrollar un modelo de machine learning para predecir el número de pedidos de taxi por hora para la empresa **Sweet Lift Taxi**. Al predecir la demanda con precisión, la empresa puede optimizar la distribución de sus conductores, reducir los tiempos de espera de los pasajeros y aumentar la eficiencia operativa. Para lograr esto, se entrenaron y evaluaron varios modelos de regresión en función de su **Error Cuadrático Medio (RMSE)**, con un umbral de rendimiento establecido en **48 RMSE**.  

## **Preparación y Preprocesamiento de Datos**  

### **Selección de Características y Variable Objetivo**  
El conjunto de datos contenía múltiples características relacionadas con los pedidos de taxi. Se realizó la división de la siguiente manera:  

- **Variable objetivo (`X`)**: El número de pedidos de taxi (`num_orders`).  
- **Características (`y`)**: Todas las demás variables excepto `num_orders`.  

### **División en Conjuntos de Entrenamiento y Prueba**  
Se dividió el conjunto de datos en **entrenamiento y prueba** usando **`train_test_split`**, reservando el **10% de los datos para pruebas** y asegurando que no hubiera mezcla de datos (`shuffle=False`). Posteriormente, se reestructuraron los datos para garantizar compatibilidad con los modelos.  

## **Entrenamiento y Evaluación de Modelos**  

Se entrenaron varios modelos de regresión y se realizó el ajuste de hiperparámetros utilizando **GridSearchCV** para encontrar la mejor configuración. A continuación, se detallan los modelos probados, sus configuraciones y resultados.  

### **Regresión Lineal**  
El modelo de **Regresión Lineal** sirvió como base inicial. Los resultados fueron:  
- **RMSE en entrenamiento**: No especificado  
- **RMSE en prueba**: **53.2** (superior al umbral de 48)  

Dado que el modelo no cumplió con el umbral requerido, se exploraron alternativas.  

### **Random Forest Regressor**  
Se entrenó un **Random Forest Regressor** con los siguientes valores:  
- `n_estimators`: [50, 100, 200, 300, 500]  
- `max_depth`: [10, 20, 50, 100]  

Los mejores parámetros seleccionados fueron **`n_estimators=200, max_depth=10`**, obteniendo:  
- **RMSE en entrenamiento**: No especificado  
- **RMSE en prueba**: **46.3**  

Este modelo cumplió con el umbral de rendimiento, por lo que fue considerado viable.  

### **LightGBM Regressor**  
Se entrenó el **LightGBM Regressor** con:  
- `n_estimators`: [50, 100, 200, 300, 500]  
- `max_depth`: [10, 20, 50, 100]  
- `num_leaves`: [10, 20, 50, 100]  

La mejor configuración (**`n_estimators=200, max_depth=10, num_leaves=50`**) arrojó:  
- **RMSE en entrenamiento**: No especificado  
- **RMSE en prueba**: **46.2**  

### **CatBoost Regressor**  
Para **CatBoost**, se probaron los siguientes hiperparámetros:  
- `iterations`: [100, 200, 500]  
- `depth`: [5, 10, 15]  

La mejor configuración fue **`iterations=500, depth=5`**, logrando los mejores resultados entre todos los modelos:  
- **RMSE en entrenamiento**: No especificado  
- **RMSE en prueba**: **44.7**  

### **XGBoost Regressor**  
Se probó el **XGBoost Regressor** con:  
- `n_estimators`: [None, 30, 50, 100]  
- `max_depth`: [None, 5, 10, 20]  

La mejor combinación (**`n_estimators=30, max_depth=5`**) resultó en:  
- **RMSE en entrenamiento**: No especificado  
- **RMSE en prueba**: **47.0**  

## **Comparación del Rendimiento de los Modelos**  

| Modelo                     | RMSE (Prueba) |
|---------------------------|--------------|
| **CatBoost Regressor**    | **44.7**     |
| LightGBM Regressor       | 46.2         |
| Random Forest Regressor  | 46.3         |
| XGBoost Regressor        | 47.0         |
| Regresión Lineal         | 53.2         |

- **Mejor Modelo:** **CatBoost Regressor** (RMSE: 44.7)  
- **Peor Modelo:** **Regresión Lineal** (RMSE: 53.2)  

## **Conclusión**  

Después del entrenamiento y la evaluación de los modelos, se identificó que el **CatBoost Regressor** tuvo el mejor rendimiento con un **RMSE de 44.7**, significativamente por debajo del umbral de **48 RMSE**.  

Al implementar este modelo, **Sweet Lift Taxi** podrá:  
- Predecir la demanda de taxis por hora con mayor precisión.  
- Optimizar la distribución de conductores para reducir los tiempos de espera.  
- Mejorar la satisfacción del cliente y aumentar la rentabilidad.  

En conclusión, este proyecto logró desarrollar una solución de machine learning eficaz para la predicción de la demanda de taxis, proporcionando información valiosa para que **Sweet Lift Taxi** optimice su eficiencia operativa.  
