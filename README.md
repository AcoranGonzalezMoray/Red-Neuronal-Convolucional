# Red-Neuronal-Convolucional

## Introducción
Para la realización de este proyecto se ha utilizado el siguiente dataset: ```https://www.kaggle.com/datasets/misrakahmed/vegetable-image-dataset```
Originalmente consta de 15000 imágenes de entrenamiento, 3000 para testing y otras 3000 de validación donde estaban repartidas en 15 tipos de vegetales; sin embargo, hemos reducido el numero de clases a   7 quedándonos con ```Zanahoria Papaya Tomate Papa Pimiento Brócoli  Calabaza.```  con 500 imagenes por cada clase obteniendo finalmente 3500 imagenes (2800 para entrenamiento & 700 para validación) Tras ver e indagar en este repositorio de imágenes concluimos en que era idóneo para trabajar con él.


## Entrenamiento
Aqui debemos separar 2 versiones:

### Versión 2.1 (Con Data Augmentation)

- Teniendo en cuenta que el dataset original posee 3500 nos disponemos a aumentar  la cantidad de datos agregando copias ligeramente modificadas de los  datos ya existentes o datos sintéticos recién creados a partir de datos existentes para ello se ha utilizado  ```AUGMENTOR`` es un paquete de Python diseñado para ayudar al aumento y la generación artificial de datos de imágenes. En nuestro caso hemos generado un total de 8400 imagenes (6720 para entrenamiento y 1680 para validación) introduciendo algunas de las siguientes modificaciones:

```
Probabilidad = 70% - Modificacion = Rotación (Rotación máxima hacia la izquierda/derecha 25 )
Probabilidad = 60% - Modificacion = Vuelta de la imagen de izquierda a derecha
Probabilidad = 60% - Modificacion = Vuelta de la imagen de arriba a abajo
Probabilidad = 60% - Modificacion = Vuelta de la imagen de forma aleatoria
```
- Una vez generado el nuevo dataset entramos en la Aquitectura de Capas, tanto para la versión con ```Data Augmentation``` como la  sin ```Data Augmentation``` disponen de 3 configuraciones 

```
1 Configuración:
5 Capas con (32-64-128-128-7) neuronas utilizando la función relu|softmax para las capas y aplicando un dropout de (0.25 - 0.25 - 0.5)
2 Configuración:
6 Capas con (128-128-128-128-256-7) neuronas utilizando la función relu|softmax para las capas y aplicando un dropout de (0.3 - 0.3 - 0.3 - 0.3 - 0.5 )
3 Configuración:
7 Capas con (32-64-128-256-512-512-7) neuronas utilizando la función relu|softmax para las capas y aplicando un dropout de (0.3 - 0.3 - 0.3 - 0.3 - 0.5 )
```

### Versión 2.2 (Sin Data Augmentation)

- Como se ha comentado anteriormente en esta versión también se aplica el mismo numero y tipo de configuraciones, el unico detalle a tener en cuenta es que esta versión cuenta con un numero menor de imagenes debido a que utiliza e dataset original.

## Resultados

- Teniendo en cuenta lo anterior procedemos a mostrar los resultados:
### ORIGINAL:
|Nº Conf| Nº de Capas     | Nº de Filtros x Capa            | kernelSize        | Función de Activacion | DroupOut                    | **Precisión**|
|-------|-----------------| --------------------------------|-------------------|-----------------------|-----------------------------|--------------|
|1      | 5               | 32, 64, 128, 128, 7             |3x3 3x3 3xx3       |relu, softmax          |0.25, 0.25, 0.5              |**0.9715**    |
|2      | 6               | 128, 128, 128, 128, 256, 7      |3x3 3x3 3x3 3x3 3x3|relu, softmax          |0.3, 0.3, 0.3, 0.3, 0.5      |**0.9767**    |
|3      | 7               | 32, 64, 128, 256, 512, 512, 7   |5x5 3x3 3x3 3x3 3x3|relu, softmax          |0.3, 0.3, 0.3, 0.3, 0.3, 0.5 |**0.9603**    |


|Configuración    |Graficas                         |
| --------------- | --------------------------------|
| 1               |![Image text](https://github.com/AcoranGonzalezMoray/Red-Neuronal-Convolucional/blob/main/img/1-(SIN%20AUG).png)|
| 2               |![Image text](https://github.com/AcoranGonzalezMoray/Red-Neuronal-Convolucional/blob/main/img/2-(SIN%20AUG).png)|
| 3               |![Image text](https://github.com/AcoranGonzalezMoray/Red-Neuronal-Convolucional/blob/main/img/3-(SIN%20AUG).png)| 



### DATA AUGMENTATION:
|Nº Conf| Nº de Capas     | Nº de Filtros x Capa            | kernelSize        | Función de Activacion | DroupOut                    | **Precisión**|
|-------|-----------------|---------------------------------|-------------------|-----------------------|-----------------------------|--------------|
|1      | 5               | 32, 64, 128, 128, 7             |3x3 3x3 3xx3       |relu, softmax          |0.25, 0.25, 0.5              |**0.9942**    |
|2      | 6               | 128, 128, 128, 128, 256, 7      |3x3 3x3 3x3 3x3 3x3|relu, softmax          |0.3, 0.3, 0.3, 0.3, 0.5      |**0.9660**    |
|3      | 7               | 32, 64, 128, 256, 512, 512, 7   |5x5 3x3 3x3 3x3 3x3|relu, softmax          |0.3, 0.3, 0.3, 0.3, 0.3, 0.5 |**0.9658**    |


|Configuración    |Graficas                         |
| --------------- | --------------------------------|
| 1               |![Image text](https://github.com/AcoranGonzalezMoray/Red-Neuronal-Convolucional/blob/main/img/1-(Con%20AUG).png)|
| 2               |![Image text](https://github.com/AcoranGonzalezMoray/Red-Neuronal-Convolucional/blob/main/img/2-(Con%20AUG).png)|
| 3               |![Image text](https://github.com/AcoranGonzalezMoray/Red-Neuronal-Convolucional/blob/main/img/3-(Con%20AUG).png)| 




## Conclusiones
- Bien de todos los resultados anteriores nos quedamos con:

|Nº Conf| Nº de Capas     | Nº de Filtros x Capa            | kernelSize        | Función de Activacion | DroupOut                    | **Precisión**|
|-------|-----------------|---------------------------------|-------------------|-----------------------|-----------------------------|--------------|
|1      | 5               | 32, 64, 128, 128, 7             |3x3 3x3 3xx3       |relu, softmax          |0.25, 0.25, 0.5              |**0.9942**    |

|Configuración    |Graficas                         |
| --------------- | --------------------------------|
| 1               |![Image text](https://github.com/AcoranGonzalezMoray/Red-Neuronal-Convolucional/blob/main/img/1-(Con%20AUG).png)|

### ANALISIS GRAFICA
- Analisando la gráfica observamos a simple vista que no presenta un caso de overfitting o underfitting, la linea de perdida disminuye constantemente a medida que aumenta la precision de la linea de entrenamiento y validación, estas 2 ultimas aumentan a lo largo de los epochs de forma ajustada o superpuestas lo cual es un buen indicio de que el modelo se ha entrenado correctamente. Otro dato a analizar son los picos expuestos en la gráfica, estos picos son causados principalmemte por el dropout este es un metodo que desactiva un numero de neuronas de una red neuronal de forma aleatoria. En cada iteración de la red neuronal dropout desactivara diferentes neuronas lo que obliga a las neuronas cercanas a no depender tanto de las neuronas desactivadas. 

- Si continuamos con la matriz de confución el mapa de calor forma un diagonal, lo cual indica que ha acertado la gran mayoria de predicciones,excepto en algunos casos como por ejemplo el caso 2 falla 3 predicciones.

### RESTO DE GRAFICAS QUE PRESENTAN CLARAMENTE UN MODELO DE OVERFITTING
- Si miramos el comportamiento general de estas gráficas vemos que son el característico perfecto de un modelo que presenta Overfitting. Por un lado la Accuracy de los datos de entrenamiento aumenta linealmente con las epochs, hasta alcanzar casi el 100%, mientras que la Accuracy de los datos de validación se detiene alrededor del 80% y a partir de aquí se mantiene constante a lo largo de las epochs.

¿Cómo lo evitamos?
- Entrenamiento con más datos, es posible que esta técnica no funcione todas las veces. Básicamente, ayuda al modelo a identificar mejor la señal. Pero en algunos casos, el aumento de los datos también puede significar alimentar más ruido al modelo. Cuando entrenamos el modelo con más datos, debemos asegurarnos de que los datos estén limpios y libres de aleatoriedad e inconsistencias.

- Detención anticipada, cuando el modelo se está entrenando, puedes medir el rendimiento del modelo en función de cada iteración. Podemos hacer esto hasta un punto en el que las iteraciones mejoren el rendimiento del modelo. Después de esto, el modelo sobreajusta los datos de entrenamiento a medida que la generalización se debilita después de cada iteración. Entonces, básicamente, la detención anticipada significa detener el proceso de entrenamiento antes de que el modelo pase el punto donde el modelo comienza a sobreajustarse a los datos de entrenamiento. Esta técnica se utiliza principalmente en el aprendizaje profundo.

- Aplicar un dropout correctamente.

### Terminos y Notas del Código

- **Capas Convolutivas** , una capa de este tipo aplica un filtro o kernel a una región determinada de la imagen, siendo 3x3 o 5x5 píxeles los tamaños más usuales, permitiendo extraer características locales de la imagen, al estar relacionando píxeles cercanos. Pero además, según profundizamos en la red se va reduciendo el tamaño de la imagen que circula por ella, con lo cual capas más profundas van a relacionar píxeles que corresponden a secciones más alejadas en la imagen inicial.

- **Pooling** , es el segundo elemento fundamental de estas redes, normalmente se utilizan dos: average pooling y max pooling, lo que hacen estas capas es, para un tamaño dado (por ejemplo, 2x2 píxeles) reducir cada región del input de ese tamaño a un único píxel con el valor medio/máximo. La principal utilidad es la de reducir el tamaño de la imagen según avanzamos en la red, ya que aunque las capas convolucionales ya lo reducen, normalmente queremos hacerlo más rápido y así reducir el número de operaciones.

- **Capas Densas** , las dos capas anteriores son los building blocks de la parte de extracción de características de las imágenes, pero una vez hemos extraído esta información, hace falta otro tipo de capa que pese estas características y clasifique la imagen en nuestras clases. Estas son las capas densas. Las capas densas son las capas típicas de las redes neuronales, conectan todos los elementos del input (un vector) con todos los del output (otro vector), para lo cual necesitaremos “aplanar” la imagen que sale de nuestra última capa convolucional.


- **Dropout** , es un metodo que desactiva un numero de neuronas de una red neuronal de forma aleatoria. En cada iteración de la red neuronal dropout desactivara diferentes neuronas, las neuronas desactivadas no se toman en cuenta para el forwardpropagation ni para el backwardpropagation lo que obliga a las neuronas cercanas a no depender tanto de las neuronas desactivadas. Este metodo ayuda a reducir el overfitting ya que las neuronas cercanas suelen aprender patrones que se relacionan y estas relaciones pueden llegar a formar un patron muy especifico con los datos de entrenamiento, con dropout esta dependencia entre neuronas es menor en toda la red neuronal, de esta manera la neuronas necesitan trabajar mejor de forma solitaria y no depender tanto de las relaciones con las neuronas vecinas (en las capas de entrada suele usarse un dropout muy alto (0.7) para mantener a la mayoria de neuronas activadas y en capas ocultas un dropout de (0.5).

- **Activacion** , las funciones de activación no son específicas de las CNNs sino de cualquier tipo de red neuronal. Normalmente se aplican después de cada capa, y permiten tener elementos no lineales, que es lo que da a las redes neuronales su capacidad predictiva.


- **Overfitting** , en resumen, con Overfitting o sobreajuste, nos referimos a lo que le sucede a un modelo cuando este modela los datos de entrenamiento demasiado bien, aprendiendo detalles de estos que no son generales. Esto es debido a que sobreentrenamos nuestro modelo y este estará considerando como válidos solo los datos idénticos a los de nuestro conjunto de entrenamiento, incluidos sus defectos (también llamado ruido en nuestro contexto). Es decir, nos encontramos en la situación que el modelo puede tener una baja tasa de error de clasificación para los datos de entrenamiento, pero no se generaliza bien a la población general de datos en los que estamos interesados en realidad. Es evidente que, en general, esta situación presenta un impacto negativo en la eficiencia del modelo cuando este se usa para inferencia con datos nuevos. Por ello es muy importante evitar estar en esta situación y de aquí la utilidad de reservar una parte de datos de entrenamiento como datos de validación para poder detectar esta situación.


- **Underitting** ,si “overfitting” o “sobreajuste” es lo que sucede cuando el modelo presta atención en demasía a los datos, hasta el punto en el que es incapaz de discernir qué es señal y qué es ruido o, en otras palabras, qué es importante y qué no, entonces “underfitting” es lo que ocurre cuando nuestro modelo es muy simplista, insuficiente para capturar los matices, particularidades y complejidades en los datos. (Entrenamiento y validacion dismminuye de forma constante)

### Autores
<li>Acorán González Moray</li>
<li>Alejandro Vialard Santana</li>








