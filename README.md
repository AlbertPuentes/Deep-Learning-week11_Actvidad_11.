# Deep-Learning-week11_Actvidad_11.

#  Conclusiones

### 1. Análisis del comportamiento del modelo

* El modelo LSTM implementado logra capturar la tendencia general de la serie temporal. Al analizar la gráfica de predicciones versus los valores reales, se puede observar que la línea de predicción sigue de cerca los movimientos estructurales del precio de la acción. Sin embargo, en escenarios de **alta volatilidad** (picos pronunciados o caídas abruptas), el modelo suele presentar un ligero retraso o desfasamiento. Esto es un comportamiento estadísticamente normal, ya que la red basa su predicción en una ventana temporal previa (en este caso, de 60 días), lo que ocasiona que el modelo ajuste su proyección *después* de que el evento disruptivo ya comenzó a ocurrir.
 

### 2. Identificación de posibles problemas: Sobreajuste y Generalización

* **Sobreajuste (Overfitting):** Durante el entrenamiento, si se observa en las curvas de aprendizaje que la pérdida de validación (`val_loss`) comienza a incrementar mientras la pérdida de entrenamiento (`loss`) sigue disminuyendo, estamos ante un claro caso de sobreajuste. En nuestra arquitectura, mitigamos este riesgo utilizando capas de `Dropout(0.2)`, las cuales desactivan aleatoriamente el 20% de las conexiones neuronales en cada época, forzando a la red a no depender de patrones ruidosos específicos de los datos de entrenamiento.
* **Límites de Generalización en Finanzas:** Aunque el modelo alcance un bajo error cuadrático medio, predecir mercados bursátiles tiene limitaciones inherentes. El modelo LSTM es excelente identificando la autocorrelación de la serie y su estacionalidad, pero es incapaz de prever choques externos o estocásticos (noticias geopolíticas, cambios de tasas de interés o crisis globales). El modelo generaliza bien los patrones matemáticos del histórico, pero carece del contexto fundamental del mundo real.


### 3. Conclusiones técnicas

1.  **Idoneidad de la arquitectura LSTM:** Las Redes Neuronales Recurrentes, y en particular la variante **Long Short-Term Memory**, demuestran ser herramientas sumamente potentes para el modelado de datos secuenciales. Su mecanismo de "puertas" (gates) y su estado de celda interno les permiten retener memoria a largo plazo y mitigar el problema del desvanecimiento del gradiente, características vitales al trabajar con series de tiempo.
2.  **Importancia crítica del preprocesamiento:** El desempeño de la red depende enteramente de la preparación de los datos. El escalado (normalización de 0 a 1) garantiza la estabilidad y velocidad de convergencia de la red, mientras que la estructuración mediante "ventanas temporales deslizantes" es lo que permite convertir un conjunto de datos continuo en un problema de aprendizaje supervisado tradicional.
3.  **Superioridad frente a métodos clásicos:** Desde una perspectiva técnica de *Machine Learning*, este ejercicio evidencia que las redes neuronales pueden aprender y proyectar relaciones no lineales mucho más complejas que los modelos estadísticos tradicionales (como ARIMA), siendo especialmente útiles cuando se dispone de grandes volúmenes de datos históricos.
