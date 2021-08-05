---
title: Umbralización openCV python
date: 2021-08-03 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, umbralización, thresholding , simple, adaptativo, otsus]  
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_350/v1628110013/kipunaEC/umbralizar/UMBRALES_rq091l.gif
---

***

# Umbralización o thresholding

Consiste en modificar una imagen a una representación binaria, por medio de la modificación de los valores de los pixeles estableciendo un valor umbral.

![umbralizar](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1628081360/kipunaEC/umbralizar/umbralizacion1_vjfzbd.png)
_Fig 1. Izq. Imagen original. Der. Umbral o threshold con el método de Otzuu_

# Umbralización simple

La umbralización simple consiste el modificar el valor de un píxel si sobrepasa el umbral establecido. Existen varios tipos de umbralización simple establecidos en la [documentación de openCV](https://docs.opencv.org/4.5.2/d7/d4d/tutorial_py_thresholding.html) como: 
[THRESH_BINARY](#THRESH_BINARY),
[THRESH_BINARY_INV](#THRESH_BINARY_INV), 
[THRESH_TRUNC](#THRESH_TRUNC), 
[THRESH_TOZERO](#THRESH_TOZERO),
[THRESH_TOZERO_INV](#THRESH_TOZERO_INV) 

Para describir la umbralización simple en este ejemplo uso la imagen que se muestra en *Fig 2* que es una imagen en escala de grises que matiza desde 0 a 255. Como mostré en un post anterior [Crear una imagen BGR openCV](../Crear-una-imagen-BGR-openCV-Python/), puedo ver los valores de los píxeles haciendo zoom con openCV (Si no puedes hacer zoom el los pixeles, ejecuta tu código en un [entorno virtual conda](../Como-crear-un-entorno-virtual-con-conda-para-python-en-Windows/). 

![matrizGris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_200/v1628081877/kipunaEC/umbralizar/matizGris_slneyu.png)
_Fig 2. Matiz de gris_

Los píxeles de tonalidad más oscura estarán cerca de `0` y los más claros cerca de `255`

![cercanos](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_550/v1628085656/kipunaEC/umbralizar/cercanos0255_rco5sb.png)
_Fig 3. Píxeles cercanos a 0 son más oscuros, píxeles cercanos a 255 son más claros_

## Función cv2.threshold 

Para aplicar la umbralización simple se usa el siguiente comando en python:

```python
ret,thresh = cv2.threshold(img, umbral, valorMax , tipo)
```
Los parámetros son los siguientes:
1. `img` es la imagen gris que va a ser analizada
2. `umbral` es el valor indicado a analizar en cada píxel
3. `valorMax` Valor que se coloca a un píxel si sobrepasa el umbral 
4. `tipo` se elige un tipo de umbralización: `THRESH_BINARY`, `THRESH_BINARY_INV`, `THRESH_TRUNC`, `THRESH_TOZERO]`, `THRESH_TOZERO_INV`, `THRESH_OTSU`. 

La función devuelve:

1. `thresh` imagen binarizada
2. `ret` valor del umbral

Como se ve en *Fig 4* aproximadamente los píxeles por donde pasa la línea punteada tendrán el valor de `100`. En los siguientes ejemplos considero que el umbral es 100, lo que significa que se verán cambios en la umbralización a la derecha e izquierda de la línea punteada.

![tiposUbral](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_350/v1628092642/kipunaEC/umbralizar/umbrales_bhedfq.png)
_Fig 4. Posición del Umbral 100_


## Umbralización simple - formulas

En los documentos [openCV](https://docs.opencv.org/4.5.2/d7/d4d/tutorial_py_thresholding.html) se encuentra esta tabla que muestra como funciona la umbralización simple. 

![tiposUmbral](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1628092278/kipunaEC/umbralizar/umbralizaciones_ogwkbo.png)
_Fig 5. Fórmulas Umbralización simple_


## THRESH_BINARY
El resultado que se obtiene en *Fig 6* se asocia con la fórmula de *Fig 5* para `THRESH_BINARY`. Y muestra que, si el píxel (`src(x,y)`) supera el umbral (`thresh`), en la imagen binarizada a los píxeles que superaron el umbral se les asigna el valor máximo establecido (`maxval` en este ejemplo es 255). A continuación el código.

```python
import cv2
from matplotlib import pyplot as plt

img = cv2.imread('matriz.png',0)

ret,thresh1 = cv2.threshold(img,100,255,cv2.THRESH_BINARY)

#Grafico adyacente de figuras
images = [img, thresh1]
titles = ['Escala de Gris','THRESH_BINARY']
for i in range(2):
    plt.subplot(1,2,i+1)
    plt.imshow(images[i],'gray',vmin=0,vmax=255)
    plt.title(titles[i])
    plt.xticks([]),plt.yticks([])
plt.show()
```
Los píxeles que superaron el valor de `100`, ahora son todos `255` y los que no superaron el umbral ahora tiene el valor de `0`

![tiposUmbral](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1628091579/kipunaEC/umbralizar/Original-THRESH_BINARY_lwlnsd.jpg)
_Fig 6.THRESH_BINARY_

## THRESH_BINARY_INV

El resultado que se obtiene en *Fig 7* se asocia con la fórmula de *Fig 5* para `THRESH_BINARY_INV`. Y muestra que, si el píxel (`src(x,y)`) supera el umbral (`thresh`), en la imagen binarizada a los píxeles que superaron el umbral se les asigna cero `0` y a los que no superaron el umbral se les asigna el valor máximo establecido (`maxval` en este ejemplo es 255). A continuación el código. Como su nombre lo indica es el inverso de `THRESH_BINARY_INV`

```python
ret,thresh2 = cv2.threshold(img,100,255,cv2.THRESH_BINARY_INV)
```
![binaryTHRESH_BINARY_INV-inv](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1628091579/kipunaEC/umbralizar/Original-THRESH_BINARY_INV_xzjqnu.jpg)
_Fig 7.THRESH_BINARY_INV_

## THRESH_TRUNC
El resultado que se obtiene en *Fig 8* es una imagen en escala de grises y se asocia con la fórmula de *Fig 5* para `THRESH_TRUNC`. Estas muestran que, si el píxel (`src(x,y)`) supera el umbral (`thresh`), en la imagen binarizada a los píxeles que superaron el umbral se les asigna el mismo valor del **umbral** y a los que no superaron el umbral se les asigna los mismos valores que tenían originalmente. A continuación el código.

```python
ret,thresh3 = cv2.threshold(img,100,255,cv2.THRESH_TRUNC)
```
![THRESH_TRUNC](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1628091579/kipunaEC/umbralizar/Original-THRESH_TRUNC_w9ajp8.jpg)
_Fig 8.THRESH_TRUNC_

## THRESH_TOZERO
El resultado que se obtiene en *Fig 9* se asocia con la fórmula de *Fig 5* para `THRESH_TOZERO`. Y muestra que, si el píxel (`src(x,y)`) supera el umbral (`thresh`), en la imagen binarizada a los píxeles que superaron el umbral mantienen el valor de los pixeles originalmente, y cuando no superan el umbral se les asigna cero.  A continuación el código.

```python
ret,thresh4 = cv2.threshold(img,100,255,cv2.THRESH_TOZERO)
```
![THRESH_TOZERO](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1628091579/kipunaEC/umbralizar/Original-THRESH_TOZERO_apqjdb.jpg)
_Fig 9.THRESH_TOZERO_
## THRESH_TOZERO_INV
El resultado que se obtiene en *Fig 10* se asocia con la fórmula de *Fig 5* para `THRESH_TOZERO_INV`. Y muestra que, si el píxel (`src(x,y)`) supera el umbral (`thresh`), en la imagen binarizada a los píxeles que superaron el umbral se les asigna cero, y a los píxeles que no superaron el umbral se les asigna el mismo valor que originalmente tenías. A continuación el código.

```python
ret,thresh5 = cv2.threshold(img,100,255,cv2.THRESH_TOZERO_INV)
```

![THRESH_TOZERO_INV](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1628091579/kipunaEC/umbralizar/Original-THRESH_TOZERO_INV_uhvcyn.jpg)
_Fig 10. THRESH_TOZERO_INV_

# Umbralización adaptativa

*Fig 11* es una imagen que usare para mostrar como puede mejorar la umbralización con un método adaptativo.

![THRESH_TOZERO_INV](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1628096728/kipunaEC/umbralizar/libro_itdr6o.jpg)
_Fig 11. Imagen con diferentes todos de iluminación_

Si aplico umbralización simple a *Fig11*, se verá como se muestra en *Fig12*, pero con umbralización adaptativa puedo encontrar mejores resultados.

![THRESH_BINARY](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1628097697/kipunaEC/umbralizar/adaptativoBinario_wrpg4i.png)
_Fig 12. Imagen con diferentes todos de iluminación_

A diferencia de la umbralización simple, la umbralización adaptativa no tendrá un valor umbral establecido. Sino que el "algoritmo determina el umbral de un píxel en función de una pequeña región a su alrededor. Entonces obtenemos diferentes umbrales para diferentes regiones de la misma imagen, lo que brinda mejores resultados para imágenes con iluminación variable" [^1]. 

Se puede seleccionar entre dos métodos adaptativos, que son los que deciden como se va a calcular el valor umbral:
1. `cv.ADAPTIVE_THRESH_MEAN_C`
2. `cv.ADAPTIVE_THRESH_GAUSSIAN_C`

```python
threshold = cv2.adaptiveThreshold(img,maxValue,adaptiveMethod,thresholdType,blockSize,C)
```
Donde:
1. `img` es una imagen de un solo canal, debe ser en escala de grises
2. `maxValue` valor asignado a los pixeles cuando cumplen la condición
3. `adaptiveMethod` método adaptativo, se elige entre `cv.ADAPTIVE_THRESH_MEAN_C`, `cv.ADAPTIVE_THRESH_GAUSSIAN_C`
4. `thresholdType` elegir un método de umbralización
5. `blockSize` Tamaño de una vecindad de píxeles que se utiliza para calcular un valor de umbral para el píxel: 3, 5, 7, etc
6. `C`  Constante restada de la media o media ponderada

El código a continuación, muestra como la umbralización adaptativa funciona. El tamaño del bloque lo establezco como `11` y la contante C como `2` siguiendo el ejemplo de [openCV documents](https://docs.opencv.org/4.5.2/d7/d4d/tutorial_py_thresholding.html), pero más adelante probaré con otros valores.

```python
import cv2
from matplotlib import pyplot as plt

img = cv2.imread('libro.jpg',0)

th1 = cv2.adaptiveThreshold(img,255,cv2.ADAPTIVE_THRESH_MEAN_C,cv2.THRESH_BINARY,11,2)
th2 = cv2.adaptiveThreshold(img,255,cv2.ADAPTIVE_THRESH_GAUSSIAN_C,cv2.THRESH_BINARY,11,2)

#Grafico adyacente de figuras
images = [th1, th2]
titles = ['ADAPTIVE_THRESH_MEAN_C', 'ADAPTIVE_THRESH_GAUSSIAN_C']
for i in range(2):
    plt.subplot(1,2,i+1)
    plt.imshow(images[i],'gray',vmin=0,vmax=255)
    plt.title(titles[i])
    plt.xticks([]),plt.yticks([])
plt.show()
```

![adaptatiev1](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1628098105/kipunaEC/umbralizar/adapattive112_nlqik2.png)
_Fig 13. Umbral adaptativo. BlockSize = 11, C = 2_

En *Fig 14* se usa un tamaño de bloque `11` y una constate `10`

![adaptatiev1](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1628098101/kipunaEC/umbralizar/adaptative1110_jozcdc.png)
_Fig 14. Umbral adaptativo. BlockSize = 11, C = 10_

En *Fig 15* se usa un tamaño de bloque `15` y una constate `10`

![adaptatiev1](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1628098103/kipunaEC/umbralizar/adaptative1510_tpgcit.png)
_Fig 15. Umbral adaptativo. BlockSize = 15, C = 10_

Se puede probar con varios valores y comparar el funcionamiento

# Binarización método de Otsu

A diferencia del la umbralización simple, Otsu calcula automáticamente un umbral para toda la imagen. Y a diferencia de la umbralización adaptativa, el umbral es el mismo en toda la imagen y no varía por regiones.

La *Fig 16* muestra como Otsu funciona, a continuación el código.

```python
import cv2
from matplotlib import pyplot as plt

img1 = cv2.imread('libro.jpg',0)
img2 = cv2.imread('quito.jpg',0)
img3 = cv2.imread('matriz.png',0)

ret1, th1 = cv2.threshold(img1,100,255,cv2.THRESH_BINARY+cv2.THRESH_OTSU)
ret2, th2 = cv2.threshold(img2,40,255,cv2.THRESH_BINARY+cv2.THRESH_OTSU)
ret3, th3 = cv2.threshold(img3,100,255,cv2.THRESH_BINARY+cv2.THRESH_OTSU)

print('Umbral de th1:', ret1)
print('Umbral de th2:', ret2)
print('Umbral de th3:', ret3)

images = [img1, th1, img2, th2, img3, th3]
titles = ['libro', 'THRESH_OTSU', 'quito', 'THRESH_OTSU', 'matiz', 'THRESH_OTSU']

for i in range(6):
    plt.subplot(3,2,i+1)
    plt.imshow(images[i],'gray',vmin=0,vmax=255)
    plt.title(titles[i])
    plt.xticks([]),plt.yticks([])
plt.show()
```
![otsu](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_400/v1628108376/kipunaEC/umbralizar/otsu3_ourooh.png)
_Fig 17. Binarización método otsu_

Inicialmente los valores del umbral los establecí aleatoriamente, y luego al ejecutar el método de Otsu, en la consola se imprime los valores del umbral que estableció automáticamente el algoritmo de Otzu.
Puse 3 imágenes para ver como el algoritmo encuentra diferentes umbrales.

```terminal
Umbral de th1: 150.0
Umbral de th2: 95.0
Umbral de th3: 140.0
```

*** 

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: OpenCV documentación. *Image Thresholding*. [https://docs.opencv.org/4.5.2/d7/d4d/tutorial_py_thresholding.html](https://docs.opencv.org/4.5.2/d7/d4d/tutorial_py_thresholding.html)

