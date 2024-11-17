1. Introducci�n
El presente informe analiza modelos de clasificaci�n (1D/tabular, 2D/im�genes, late-fusion y early-fusi�n) desarrollados para abordar un problema de clasificaci�n, enfrentando un desaf�o com�n de sobreajuste. Se implementaron diversas estrategias de regularizaci�n para mitigar este fen�meno y mejorar la generalizaci�n de los modelos.
2. Modelo Tabular: An�lisis de Hiperpar�metros y Regularizaci�n
2.1 Descripci�n del Modelo
* Red neuronal con capas densas
* Objetivo: Clasificaci�n de datos tabulares
2.2 T�cnicas de Regularizaci�n
1. Regularizaci�n L2
* Penalizaci�n de pesos grandes
* Prevenci�n de complejidad excesiva
2. Early Stopping
* Detenci�n del entrenamiento cuando no hay mejora
* Restauraci�n de mejores pesos
2.3 Resultados de Hiperpar�metros
Tasa de Aprendizaje
Tama�o del Lote
Precisi�n Entrenamiento
Precisi�n Validaci�n
Precisi�n Prueba
0.001
32
0.7471
0.6470
0.6906
0.005
32
0.7061
0.6262
0.6683
0.01
32
0.6997
0.6054
0.6603
2.4 An�lisis de Resultados
* Tasa de aprendizaje m�s baja (0.001) mostr� mejor rendimiento
* Tama�o de lote peque�o (32) m�s efectivo
* Regularizaciones ayudaron a controlar el sobreajuste
3. Modelo de Im�genes: Arquitectura ResNet50 y Regularizaci�n
3.1 Modelos Desarrollados
1. Modelo 1: Transfer Learning
* Congelamiento total de capas
* Precisi�n entrenamiento: 80.83%
* Precisi�n validaci�n: 55.43%
2. Modelo 2: Transfer Learning con Batch Size Diferente
* Batch size: 128
* Precisi�n entrenamiento: 88.50%
* Precisi�n validaci�n: 52.56%
3. Modelo 3: Fine Tuning
* Descongelamiento de �ltimas 10 capas
* Precisi�n entrenamiento: 93.72%
* Precisi�n validaci�n: 48.72%
3.2 T�cnicas de Regularizaci�n
1. Regularizaci�n L2
2. Dropout
3. Transfer Learning
* Congelamiento/descongelamiento selectivo de capas
3.3 An�lisis Comparativo
Modelo
Precisi�n Entrenamiento
Precisi�n Validaci�n
Precisi�n Prueba
Nivel de Sobreajuste
Modelo 1
80.83%
55.43%
51.99%
Moderado
Modelo 2
88.50%
52.56%
52.95%
Alto
Modelo 3
93.72%
48.72%
46.73%
Muy Alto
4. Modelos de Fusi�n: Mitigaci�n del Sobreajuste
4.1 Modelos Individuales
* Modelo Tabular
* Precisi�n prueba: 0.6906
* Modelo de Im�genes
* Precisi�n prueba: 0.5295
4.2 Estrategias de Fusi�n y Regularizaci�n
1. Fusi�n Tard�a (Late Fusion)
* Grid Search con Random Forest
* Validaci�n Cruzada
* Weighted Average Ensemble
2. Fusi�n Temprana (Early Fusion)
* Capas de Dropout
* Early Stopping
4.3 Resultados de Fusi�n
M�todo de Fusi�n
Precisi�n Prueba
Modelo Tabular Individual
0.6906
Weighted Average Ensemble
0.6683
Fusi�n Temprana
0.6411
Grid Search con Random Forest
0.5901
Validaci�n Cruzada con Random Forest
0.5885
Modelo de Im�genes Individual
0.5295


4.4 An�lisis comparativo 
Rendimiento general:
* Modelo Tabular individual: 0.6906 (mejor rendimiento en prueba)
* Weighted Average Ensemble (Late Fusion): 0.6683 (Validation-Modelos Base )
* Early Fusion: 0.6411 (Train-Modelos Base)
* Otros enfoques de Late Fusion: < 0.60 (Train-Modelos Base)
Comparaci�n de fusi�n temprana vs. tard�a:
* La fusi�n temprana (0.6411) supera a la mayor�a de los enfoques de fusi�n tard�a, sin embargo, no logra superar al modelo tabular individual ni al Weighted Average Ensemble.
Influencia del conjunto de datos de entrenamiento:
* Early Fusion: Utiliza caracter�sticas extra�das de los modelos base en el conjunto de entrenamiento, lo que puede llevar a incorporar el sobreajuste del modelo de im�genes.
* Late Fusion (Grid Search y Validaci�n Cruzada): Tambi�n se ven afectados por el uso de predicciones de entrenamiento.
* Weighted Average Ensemble: Se beneficia del uso de predicciones de validaci�n para calcular los pesos.
Complejidad vs. Rendimiento:
* La fusi�n temprana introduce una complejidad adicional (red neuronal con capas densas) pero no logra superar los m�todos m�s simples como el modelo tabular individual o el Weighted Average Ensemble.
Mitigaci�n del sobreajuste:
* Early Fusion: Intenta mitigar el sobreajuste con capas de Dropout y Early Stopping, pero aun as� no supera al modelo tabular individual.
* Weighted Average Ensemble: Logra una mejor mitigaci�n del sobreajuste al basarse en el rendimiento de validaci�n.
5. Razones de las diferencias en rendimiento
1. Propagaci�n del sobreajuste:
* Tanto en Early Fusion como en algunos m�todos de Late Fusion, el sobreajuste del modelo de im�genes en el conjunto de entrenamiento se propaga al modelo final.
2. Capacidad de generalizaci�n:
* El modelo tabular individual y el Weighted Average Ensemble muestran una mejor capacidad de generalizaci�n..
3. Balanceo de influencias:
* El Weighted Average Ensemble logra un mejor balance entre los modelos base, mientras que la Early Fusion puede estar dando demasiado peso a caracter�sticas menos informativas.
6. Conclusiones y recomendaciones finales
1. Uso inteligente de los datos:
* El modelo tabular individual y el Weighted Average Ensemble muestran los mejores resultados, sugiriendo que el uso inteligente de los datos de validaci�n son clave.
2. Reevaluaci�n de la fusi�n temprana:
* Considerar t�cnicas para reducir la influencia del modelo de im�genes sobreajustado en la fusi�n temprana, como la regularizaci�n de caracter�sticas o la selecci�n de caracter�sticas m�s robustas.
3. Mejora del modelo de im�genes:
* Sigue siendo una prioridad mejorar este modelo para reducir el sobreajuste y potencialmente aumentar su contribuci�n positiva en cualquier esquema de fusi�n.
4. Exploraci�n de t�cnicas h�bridas:
* Investigar m�todos que combinen aspectos de fusi�n temprana y tard�a, posiblemente con una selecci�n din�mica de caracter�sticas o modelos basada en el rendimiento de validaci�n.
5. An�lisis detallado de errores:
* Examinar los casos donde cada enfoque de fusi�n falla o acierta para entender mejor sus fortalezas y debilidades espec�ficas.
En resumen, aunque la fusi�n temprana muestra un rendimiento razonable, no logra superar al modelo tabular individual ni al Weighted Average Ensemble. Esto sugiere que, para este problema espec�fico, los enfoques que hacen un uso inteligente de los datos de validaci�n son m�s efectivos. La clave para mejorar el rendimiento general parece estar en refinar el modelo de im�genes y en desarrollar m�todos de fusi�n que puedan aprovechar las fortalezas de ambos modelos base de manera m�s efectiva.
