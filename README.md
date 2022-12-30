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

| Nº de Capas     | Nº de Filtros x Capa            | Función de Activacion | DroupOut                    | Precisión |
| --------------- | --------------------------------|-----------------------|-----------------------------|----------|
| 5               | 32, 64, 128, 128, 7             |relu, softmax          |0.25, 0.25, 0.5              |0.9942    |
| 6               | 128, 128, 128, 128, 256, 7      |relu, softmax          |0.3, 0.3, 0.3, 0.3, 0.5      |0.9767    |
| 7               | 32, 64, 128, 256, 512, 512, 7   |relu, softmax          |0.3, 0.3, 0.3, 0.3, 0.3, 0.5 |0.9603    |








## Conclusiones
