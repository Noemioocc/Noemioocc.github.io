---
title: Dibujar formas básicas openCV - python
date: 2021-01-21 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, formas, funciones, dibujo, line, polylines, fillPoly, rectangle, circle, arrowedLine]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_400/v1612454967/kipunaEC/imagen-texto/formas_yxzou9.gif
---

***

## Formas en openCV python

En esta sección para graficar formas, se genera un arreglo como se explica en el post [crear una imagen BGR en openCV](../Crear-una-imagen-BGR-openCV-Python/) y se dibuja sobre la imagen creada como arreglo.

## Dibujar una línea openCV **line** 

[line](https://docs.opencv.org/master/d6/d6e/group__imgproc__draw.html#ga7078a9fae8c7e7d13d24dac2520ae4a2) es una función de openCV que dibuja una línea uniendo dos puntos, sus parámetros son:
```python
 cv2.line(img, punto1Linea1, punto2Linea1 , colorLinea1, grosorLinea1 )
```
El código que generó **Fig 1** se describe a continuación

```python
#Importar librería cv2
import cv2
import numpy as np

#Crea una imagen con tres canales
img = np.ones((700,800,3),np.uint8)
#Establece un mismo color BRG para todos los píxeles de fondo
img[:,:,:] = [137,86,50]

#Características de línea1
punto1Linea1 = (100,100)
punto2Linea1 = (650,100)
colorLinea1 = (0,255,0)
grosorLinea1 = 10

#Características de línea2
punto1Linea2 = (200,200)
punto2Linea2 = (600,600)
colorLinea2 = (0,255,0)
grosorLinea2 = 25

#Dibujar linea
cv2.line(img, punto1Linea1, punto2Linea1 , colorLinea1, grosorLinea1 )
cv2.line(img, punto1Linea2, punto2Linea2 , colorLinea2, grosorLinea2 )

#Guardar imagen
cv2.imwrite('line.jpg', img)
```

![texto-varios-gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_400/v1612382690/kipunaEC/imagen-texto/line_oojnxv.jpg)
_Fig 1. Líneas_

## Dibujar polylínea y relleno openCV - polylines, fillPoly 

[Polylines](https://docs.opencv.org/master/d6/d6e/group__imgproc__draw.html#ga07d2f74cadcf8e305e810ce8eed13bc9) es una función que traza líneas conectadas según los puntos que se especifiquen, el tercer parámetro de `polylines` es de tipo `bool` e indica si la línea es cerrada con `True` o si la polyLínea queda abierta con `False`:

```python
cv2.polylines(img , [puntos] , True , color, grosor )
```


[fillPoly](https://docs.opencv.org/master/d6/d6e/group__imgproc__draw.html#ga8c69b68fab5f25e2223b6496aa60dad5) rellena la polylinea, los parámetros son:

```python
cv2.fillPoly(img , [puntos] , color )
```

El siguiente código generó **Fig 2**

```python
#Importar librería cv2
import cv2
import numpy as np

#Crea una imagen con tres canales
img = np.ones((700,800,3),np.uint8)
#Establece un mismo color BRG para todos los píxeles de fondo
img[:,:,:] = [192,192,80]

#Características de polyLinea1
puntos1 = np.array([[400, 50],  [200, 200], [600, 200]])
color1 = (255,50,50)
grosor1 = 5

#Características de polyLinea2 y relleno
puntos2 = np.array([ [200,350] , [100,400] , [100,500] , [200,550] , [300,500] , [300,400] ])
color2 = (50,200,50)
color22 = (118,27,190)
grosor2 = 30

#Características de fillPoly3
puntos3 = np.array([ [600,350] , [500,400] , [500,500] , [600,550] , [700,500] , [700,400] ])
color3 = (23,139,255)

#Dibujar polylinea1
cv2.polylines(img,[puntos1] , True, color1, grosor1 )

#Dibujar polylinea2 y relleno
cv2.polylines(img,[puntos2] , True, color2, grosor2 )
cv2.fillPoly(img,[puntos2] ,  color22 )

#Dibujar fillPoly
cv2.fillPoly(img,[puntos3] ,  color3 )

#Guardar imagen
cv2.imwrite('line.jpg', img)

#Mostrar imagen
cv2.imshow('polylineas',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![polyLínea](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612410621/kipunaEC/imagen-texto/line_txft1n.jpg)
_Fig 2. Formas con polyLínea y fillPoly_

## Dibujar rectángulos - rectangle

Los parámetros de [rectangle](https://docs.opencv.org/3.4/d6/d6e/group__imgproc__draw.html#ga07d2f74cadcf8e305e810ce8eed13bc9) son:

```python
cv2.rectangle(img, punto1Rectangulo, punto2Rectangulo , colorLinea, grosor, tipolinea)
```
*Nota: si se usa el tipo de línea FILLED, se debe omitir el grosor*

A continuación se describe el codigo que generó **Fig 3**
```python
#Importar librería cv2
import cv2
import numpy as np

#Crea una imagen con tres canales
img = np.ones((700,800,3),np.uint8)
#Establece un mismo color BRG para todos los píxeles de fondo
img[:,:,:] = [242,211,255]

#Tipo linea
tipolinea1 = cv2.FILLED
tipolinea2 = cv2.LINE_4
tipolinea3 = cv2.LINE_8
tipolinea4 = cv2.LINE_AA

#Características de rectángulo
punto1Rectangulo1 = (100,50)
punto2Rectangulo1 = (400,150)
color1 = (207,189,37)

#Características de rectángulo
punto1Rectangulo2 = (400,200)
punto2Rectangulo2 = (700,300)
color2 = (151,37,207)

#Características de rectángulo
punto1Rectangulo3 = (100,350)
punto2Rectangulo3 = (400,450)
color3 = (121,227,32)

#Características de rectángulo
punto1Rectangulo4 = (400,500)
punto2Rectangulo4 = (700,600)
color4 = (20,219,146)

cv2.rectangle(img, punto1Rectangulo1, punto2Rectangulo1 , color1, tipolinea1)
cv2.rectangle(img, punto1Rectangulo2, punto2Rectangulo2 , color2, tipolinea2)
cv2.rectangle(img, punto1Rectangulo3, punto2Rectangulo3 , color3, tipolinea3)
cv2.rectangle(img, punto1Rectangulo4, punto2Rectangulo4 , color4, tipolinea4)
```


![Rectángulos_](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612408607/kipunaEC/imagen-texto/line_gluxpd.jpg)
_Fig 3. Rectángulos_

## Dibujar círculos - circle

Los parámetros de [círculo](https://docs.opencv.org/3.4/d6/d6e/group__imgproc__draw.html#gaf10604b069374903dbd0f0488cb43670) son:

```python
cv2.circle(img,centro, radio, color, grosor, tipolinea )
```
*Nota: si se usa el tipo de línea FILLED, se debe omitir el grosor*

A continuación se describe el codigo que generó **Fig 4**

```python
import cv2
import numpy as np

#Crea una imagen con tres canales
img = np.ones((700,800,3),np.uint8)
#Establece un mismo color BRG para todos los píxeles de fondo
img[:,:,:] = [55,25,120]

#Tipo linea
tipolinea1 = cv2.FILLED
tipolinea2 = cv2.LINE_4
tipolinea3 = cv2.LINE_8
tipolinea4 = cv2.LINE_AA

#Características círculo1
centro1 = (200, 150)
radio1 = 80
color1 = (219, 152, 52)
grosor1 = 5

#Características círculo2
centro2 = (600, 150)
radio2 = 70
color2 = (30, 120, 25)
grosor2 = 20

#Características círculo3
centro3 = (200,500)
radio3 = 150
color3 = (160, 154, 23)
color33 = (95, 91, 5)
grosor33 = 30

#Características círculo4
centro4 = (600,450)
radio4 = 150
color4 = (20,255,130)

#Dibujar círculo1
cv2.circle(img,centro1, radio1, color1, tipolinea1 )

#Dibujar círculo2
cv2.circle(img,centro2, radio2, color2, grosor2, tipolinea2 )

#Dibujar círculo3
cv2.circle(img,centro3, radio3, color3, tipolinea1 )
cv2.circle(img,centro3, radio3, color33, grosor33, tipolinea3 )

#Dibujar círculo3
cv2.circle(img,centro4, radio4, color4, tipolinea4 )

#Guardar imagen
cv2.imwrite('line.jpg', img)

#Mostrar imagen
cv2.imshow('polylineas',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![circulo](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612451008/kipunaEC/imagen-texto/line_j2knz7.jpg)
_Fig 4. Círculos_


## Dibujar flechas - arrowedLine

Los parámetros de [arrowedLine](https://docs.opencv.org/3.4/d6/d6e/group__imgproc__draw.html#ga0a165a3ca093fd488ac709fdf10c05b2) son:

```python
cv2.arrowedLine(img,punto1Flecha, punto2Flecha, color, tipolinea, tipLength = 0.55 )
```
El parámetro `tipLength` estabece el tamaño de la flecha proporcional a la longitud de la flecha.
A continuación se describe el codigo que generó **Fig 5**

```python
import cv2
import numpy as np

#Crea una imagen con tres canales
img = np.ones((700,800,3),np.uint8)
#Establece un mismo color BRG para todos los píxeles de fondo
img[:,:,:] = [190,214,252]

#Tipo linea
tipolinea2 = cv2.LINE_4
tipolinea3 = cv2.LINE_8
tipolinea4 = cv2.LINE_AA

#Características flecha1
punto1Flecha1 = (100, 50)
punto2Flecha1 = (700, 50)
color1 = (35, 196, 81)
grosor1 = 6

#Características flecha2
punto1Flecha2 = (200, 100)
punto2Flecha2 = (100, 400)
color2 = (20,148,243)

#Características flecha3
punto1Flecha3 = (300, 150)
punto2Flecha3 = (600, 150)
color3 = (95, 91, 5)

#Características flecha3
punto1Flecha4 = (100, 425)
punto2Flecha4 = (700, 425)
color4 = (196,169,35)

#Dibujar flecha1
cv2.arrowedLine(img,punto1Flecha1, punto2Flecha1, color1, grosor1, tipolinea2 )

#Dibujar flecha2
cv2.arrowedLine(img,punto1Flecha2, punto2Flecha2, color2, tipolinea3 )

#Dibujar flecha3
cv2.arrowedLine(img,punto1Flecha3, punto2Flecha3, color3, tipolinea4 )

#Dibujar flecha4
cv2.arrowedLine(img,punto1Flecha4, punto2Flecha4, color4, tipolinea4, tipLength = 0.55 )


#Guardar imagen
cv2.imwrite('line.jpg', img)

#Mostrar imagen
cv2.imshow('polylineas',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![flechas](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612454390/kipunaEC/imagen-texto/flecha_xp6sbt.jpg)
_Fig 5. Flechas_

***

> Aprendan siempre, aprendan mucho — Mimi

***

## Referencias
1. Jeru Luke. (1 de Julio del 2018). *How to fill a polyline in OpenCV* Disponible en: [https://stackoverflow.com/questions/51121978/how-to-fill-a-polyline-in-opencv](https://stackoverflow.com/questions/51121978/how-to-fill-a-polyline-in-opencv)
2. OpenCV. *Drawing Functions*
 [https://docs.opencv.org/3.4/d6/d6e/group__imgproc__draw.html#ga57be400d8eff22fb946ae90c8e7441f9](https://docs.opencv.org/3.4/d6/d6e/group__imgproc__draw.html#ga57be400d8eff22fb946ae90c8e7441f9)
