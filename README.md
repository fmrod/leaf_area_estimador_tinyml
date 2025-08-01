**Resumen**

La agricultura es fundamental para asegurar la seguridad alimentaria,
enfrentando el reto de aumentar la productividad y la calidad de los
productos en un entorno sustentable. El propósito de la investigación
fue estimar el área foliar basada en imágenes usando inteligencia
artificial de borde. La metodología aplicada incluye cinco fases:
dominio del problema, captura de datos, desarrollo del modelo,
despliegue del modelo y prueba del modelo. Las imágenes de las hojas
fueron la fuente para generar el conjunto de datos que tiene 102
registros con las características de las hojas, tales como ancho,
altura, perímetro y área, expresadas en píxeles. El modelo tiene el
objetivo de inferir el área foliar en cm² y está basado en tres capas de
redes neuronales: una de entrada, dos ocultas y una de salida. El modelo
fue desarrollado en la plataforma Edge Impulse, desplegado sobre Arduino
Nano 33 BLE Sense y probado usando Arduino IDE. Las pruebas del modelo
versión Unoptimizaed (float32) en el dispositivo de borde tienen las
métricas de 0.009, 0.066, 0.095, 0.999 para MSE, MAE, RMSE y R\^2,
respectivamente. Se concluye que el modelo de inteligencia artificial en
el borde utilizado para estimar el área foliar tiene un significativo
rendimiento.

1.  **Introducción**

El problema principal es estimar el área foliar de las hojas de
albahaca, cuya importancia radica en su participación significativa en
el índice de área foliar. El Índice de área foliar (IAF) se expresa como
la relación entre la superficie de la hoja por unidad de área de
superficie ocupada por la planta, este índice se incrementa con el
crecimiento del cultivo hasta alcanzar un valor máximo (Carranza et al.,
2009). El presente estudio identificó cuatro variables importantes:
longitud, ancho, perímetro y área de las hojas de albahaca. La longitud
(L) se expresa como la longitud del eje mayor de la hoja medida, el
ancho (W) es la longitud del eje menor de la hoja medida, el perímetro
(P) es la longitud del contorno de la hoja medida y el área (A) es la
medidad de la superficie ocupada por la hoja.

El índice de área foliar está estrechamente relacionado con los procesos
de absorción de luz, la intercepción de agua, la evapotranspiración y la
captación de carbon entre la planta y el ambiente; por ello el monitoreo
dinámico del IAF puede proporcionar información valiosa sobre el
crecimiento de los cultivos en respuesta al ambiente y permite evaluar
el rendimiento final del cultivo (Gong et al., 2021). El índice de área
foliar está relacionado con la curva de crecimiento de la planta, cuya
variación en el tiempo está gobernada por un modelo logístico, definida
mediante la formula matemática

$af(t) = \frac{\alpha}{1 + \ e^{- k(t - \ \lambda)}}$

Donde af(t) es el valor del área foliar en función del tiempo t, α es el
tamaño máximo de la hoja (asíntota superior), cuando t 🡪∞, k es un
parámetro escalar vinculada a la tasa de crecimiento en el tiempo t y λ
es el tiempo en el se alcanza la máxima tasa de crecimiento (Colorado et
al., 2013).

La presente investigación tiene como objetivo implementar una solución
para estimar el área foliar basado en imágenes usando inteligencia
artificial en el borde.

2.  **Metodología del problema**

La metodología brinda una base fundamental para la implementación de la
solución basada en inteligencia artificial en el borde y contribuye a
desarrollar la investigación de forma sistematizada, iterativa y
consistente. En la Figura 1 se detallan las fase, objetivos y resultados
de la metodología aplicada en la investigación.

![](media/image1.png){width="6.1375in" height="2.975in"}

**Figura 1** Metodología aplicada durante la investigación

**Figura 2** Muestra del conjunto de datos de imágenes de hojas de
albahaca

**Figura 3** Calibración de la medición usando Kiamid Leafl Area
Calculador

3.  **Desarrollo del modelo**

El modelo para estimar el área foliar de las hojas de albahaca fue
desarrollado en la plataforma Edge Impulse (EI)
(<https://studio.edgeimpulse.com/>), esta plataforma ofrece un proceso
simplificado y buena experiencia de usuario. Se desarrolló el modelo de
forma iterativa hasta encontrar el modelo de estimación del área foliar
con mejor desempeño y optimizado para el dispositivo Arduino Nano 33 BLE
Sense. El desarrollo en EI consta de 6 etapas: Data Acquisition, Create
Impulse, Raw Data, Regressión, Model Testing y Deployment. En la Figura
4 se describe en alto nivel el flujo del proceso de solución completo,
usando Google Colab, Edge Impulse y Arduino IDE durante la
implementación de la solución para estimar el área foliar de la
albahaca.

**Figura 4**. Flujo del proceso de solución usando Google Colab, Edge
Impulse y Arduino IDE

La arquitectura para predecir el área foliar de hojas de albahaca está
basada en redes neuronales, con una capa de entrada que recibe las tres
características: ancho, área y perímetro expresados en pixeles, 2 capas
ocultas de 20 y 10 neuronas que usan funciones de activación RELU y una
capa de salida con función de activación Lineal que brinda el área
foliar estimada (AE), expresada en ${cm}^{2}$. En la Figura 5 se muestra
el diagram de la arquitectura de la solución basada en tres capas de
redes neuronales.

**Figura 5**. Arquitectura basado en redes neuronales para predecir el
área foliar real

4.  **Prueba del modelo**

Para las pruebas en EI se utilizaron 21 datos seleccionados
aleatoriamente del conjunto de datos. En la Tabla 1 se muestran los
resultados de las pruebas realizadas en EI, usando las dos versions del
modelo: Quantized (int8) y Unoptimizaed (float32).

**Tabla 1.** Resultados de la prueba del modelo

  ------------------------------------------------------------------------
  **Métricas**                         **Quantized          **Unoptimizaed
                                          (int8)**             (float32)**
  ---------------------------- ------------------- -----------------------
  Accuracy                                  95.24%                 100.00%

  Mean squared error (MSE)                   5.350                   0.008

  Mean absolute error (MAE)                  0.752                   0.169

  Explained variance score                   0.865                   0.996
  (R\^2)                                           
  ------------------------------------------------------------------------

En la Figura 6, se muestra el gráfico los valores de las áreas reales y
las áreas predichas por el modelo, la gran mayoria de las áreas predicha
se encuentran sobre la línea de predicción perfecta. Las métricas de las
pruebas son Error Absoluto Medio (MAE): 0.066, Error Cuadrático Medio
(MSE): 0.009, Root Mean Squared Error (RMSE): 0.095 y el coeficiente de
determinación (R²): 0.9997.

**Figura 6**. Relación del área real con el área estimada
\[${cm}^{2}\rbrack$

5.  **Conclusión**

Las métricas de 0.009, 0.066, 0.095, 0.999 para MSE, MAE, RMSE y R\^2,
respectivamente; obtenidas para el modelo versión Unoptimizaed (float32)
en Arduino Nano 33 BLE Sense permite concluir que el modelo de
inteligencia artificial en el borde utilizado para estimar el área
foliar tiene un significativo rendimiento y contribuye a la
incorporación de tecnología disruptiva en la agricultura.

**Referencias**

Carranza, C., Lanchero, O., & Miranda, D. (2009). *Análisis del
crecimiento de lechuga (Lactuca sativa L.) 'Batavia' cultivada en un
suelo salino de la Sabana de Bogotá*. *27*(1), 41--48.

Colorado, F., Montañez, I., Bolaños, C., & Rey, J. (2013). Crecimiento y
desarrollo de albahaca (Ocimum basilicum L.) bajo cubierta en la Sabana
de Bogotá. *Revista U.D.C.A Actualidad & Divulgación Científica*,
*16*(1), 121--129. https://doi.org/10.31910/rudca.v16.n1.2013.866

Gong, Y., Yang, K., Lin, Z., Fang, S., Wu, X., Zhu, R., & Peng, Y.
(2021). Remote estimation of leaf area index (LAI) with unmanned aerial
vehicle (UAV) imaging for different rice cultivars throughout the entire
growing season. *Plant Methods*, *17*(1), 1--16.
https://doi.org/10.1186/s13007-021-00789-4

Salehi, A. (2023). Kiamid Leaf Area Calculator.pdf. In *GitHub -
amarsalehi/kiamid: Leaf Area Calculators.* Salehi, Amar.
https://github.com/amarsalehi/kiamid