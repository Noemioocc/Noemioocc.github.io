---
title: Crear una imagen BGR, escala de gris openCV python
date: 2021-01-21 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, BGR, array, matriz, ones, zeros]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612369131/kipunaEC/pixeles/pixel_sxfg93.gif
---
***

## Crear una imagen en openCV python
Escribo este post porque inicialmente quería dibujar formas y texto en openCV, una de las maneras de hacerlo es [dibujar y escribir sobre una imagen](../Añadir-texto-a-una-imagen-openCV-python/) **¡realmente fue sencillo!**, pero luego surguió la interrogante, y si no quiero usar una imagen como tal (es decir leerla con `imread`) y quiero generar yo misma el fondo (crear una imagen negra, blanca, gris, etc) para escribir y dibujar formas. En esa busqueda enconté esta línea de codigo:

 `img = np.zeros((100,100,3),np.uint8)` [^1] 
 
 Usada para crear un área de `100 x 100` que representará una imagen **!ok, yo estaba de acuerdo!**, pero qué significa el `3` y `dtype=np.uint8` en esa expesión? 

* El `3` significa los canales que tiene la imagen en este caso son `B G R`. 

* `dtype=np.uint8` es el tipo de dato de cada píxel.

Bueno, para profundizar voy a empezar detallando como se representan las imágenes digitales en python y openCV.

***

## Imagen digital 

Una computadora ve las imágenes como cuadrículas con números, cada una de estas cadriculas se llama [píxel](../Pixeles-openCV-Python/), una imagen digital esta representada por la combinación de píxeles formando filas y columnas **Fig1** y **Fig2**.  

![representación-gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612321417/kipunaEC/pixeles/matrizgray_xhkxhn.jpg)
_Fig 1. Representación de píxeles en una imagen en escala de grises_

![representación-bgr](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612323012/kipunaEC/pixeles/matrizbgr_cudxc5.jpg)
_Fig 2. Representación de píxeles en una imagen BGR_

***

### **¿Cuál es la diferencia entre Fig1 (escala de grises) y Fig2 (BGR )?**

La diferencia es la cantidad de **canales** que representan a la imagen.
* En **Fig1** cada cuadrícula (píxel) tiene `1` número entre 0 a 255 y representa un canal. 
* En **Fig2** cada cuadrícula (píxel) tiene `3` números entre 0 a 255 y representan tres canales `B`, `G`, `R`.

Ahora, considerando que una imagen es una matriz de valores numerícos y que la combinación de los `3` canales `BGR` hacen que una imagen tome color, empieza a tener sentido la línea de código que mencioné al inicio `img = np.zeros((500,500,3),np.uint8)`

***

## ¿Cómo funciona **np.ones** y **np.zeros** para crear una imagen?

[ones](https://numpy.org/doc/stable/reference/generated/numpy.ones.html) y [zeros](https://numpy.org/doc/stable/reference/generated/numpy.zeros.html) son funciones de la librería [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html) para python, craen matrices  llenas de unos `1` o ceros `0` respectivamente.
Para crear una imagen en openCV recibe como parámetros: las dimensiones de la imagen `shape` y el tipo de dato de cada píxel `dtye`

```python
numpy.ones(shape, dtype)
numpy.zeros(shape, dtype)
```

1. `shape` puede ser un entero o una tupla de enteros (tupla de enteros para representar imágenes).
2. `dtpe` establece el tipo de dato del arreglo que se va a crear. *Más adelante registro como afecta el tipo de dato a la construcción de una imagen*

***

## Crear una imagen en escala de grises

En **Fig 1** y **fig 2** se representa a las imagenes numérica en forma de matriz, y para hacer esto en python y openCV uso `zeros` y `ones` porque son funciones que crean arreglos. 

En el siguiente código genera dos imágenes de color negro, el color de fondo de **Fig 3** y **Fig 4** son similares porque los valores en los píxeles son consecutivos `0` y `1`, para notar cambios en los colores los valores deben variar entre `0` a `255`

1. Importar librerías [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html), [cv2](https://opencv.org/)
2. Crear la matriz de `3`dimensiones
 * `np.zeros((6,8,1)` imagen `alto = 6`, `ancho = 8` y en cada posición estará `1` valor. Toda la matriz esta llena de `ceros`.
 * `np.ones((6,8,1)` imagen `alto = 6`, `ancho = 8` y en cada posición estará `1` valor. Toda la matriz esta llena de `ceros`.
 * `200*np.ones((6,8,1)` imagen `alto = 6`, `ancho = 8` y en cada posición estará `1` valor. Toda la matriz esta llena de `200`.

```python
#Importar librería cv2
import cv2
import numpy as np

#Crea arreglos que son la base de una imagen
img1 = np.zeros((6,8,1),np.uint8)
img2 = np.ones((6,8,1),np.uint8)
img3 = 200*np.ones((6,8,1),np.uint8)

#Mostrar imagenes
cv2.imshow('imagen-zeros',img1)
cv2.imshow('imagen-ones',img2)
cv2.imshow('imagen-250',img2)

#Cerrar las ventanas con tecla esc
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![zeros](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_250/v1611701744/kipunaEC/pixeles/zeros_lit9t2.png)
_Fig 3. Representación de una imagen, matriz 6x8 llena de ceros_


![ones](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_250/v1611701744/kipunaEC/pixeles/ones_h8sg1z.png)
_Fig 4. Representación de una imagen, matriz 6x8 llena de unos_


![200](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_250/v1612363782/kipunaEC/pixeles/200_oanpfk.jpg)
_Fig 5. Representación de una imagen, matriz 6x8 llena de 200_

*Nota: El resultado de la visualización de las imágenes del código anterior no muestra los valores de cada píxel, los valores se muestran por razones didácticas*

### Modificar el valor de píxeles en escala de grises

El color de un píxel será negro mientras sea cercano a `0` y tomará tonalidades de color blanco mientras mas sea cercano a `255`, el siguiente código muestra como se agrega valores a píxeles específicos (esta hecho con `zeros`, pero tambien funciona con `ones`) 

```python
#Importar librería cv2 y numpy
import cv2
import numpy as np

#Arreglo de zeros, es la base de una imagen
img1 = np.zeros((6,8,1),np.uint8)

#colocar valores en píxeles especìficos
img1[1,1] = 50
img1[4,4] = 200
img1[3,5] = 75
img1[2,3] = 255

#Guardo la imagen
cv2.imwrite('Img-zeros.jpg', img1)
```
![pixeles-gris-color](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_250/v1611771588/kipunaEC/pixeles/tonalidadgris_kfylxc.png)
_Fig 6. imagen de 6x8 en escala de grises, algunos píxeles fueron cambiados de tono_

***

## Crear una imagen BRG

Una imagen BGR debe ser la representación numérica de una matriz, a diferencia de la escala de grises en cada píxel existirá tres valores entre `0` y `255`  

![pixeles-gris-color](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_350/v1611697059/kipunaEC/pixeles/RGB_u7dbxt.png)
_Fig 7. Representación intuitiva de una umagen BGR_

El siguiente código genera una imagen `BGR`, creando el arreglo numérico de 3 dimensiones con las funciones `zeros` y `ones`.

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>
1. Importar librerías [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html), [cv2](https://opencv.org/)
2. Crear la matriz de `3`dimensiones
 * `np.zeros((6,8,3)` imagen `alto = 6`, `ancho = 8` y `3` canales `B G R`. Toda la matriz de `3` dimensiones esta llena de `ceros`, por lo tanto la imagen es de color negro.
 * `255*np.ones((6,8,3)` imagen `alto = 6`, `ancho = 8` y `3` canales `B G R`. Toda la matriz de `3`dimensiones esta llena de `255`, por lo tanto la imagen será de color blanco. 
 
 </details>
{::options parse_block_html="false" /} 
 

```python
#Importar librería cv2 y numpy
import cv2
import numpy as np

#Crear una imagen de color negro
img1 = np.zeros((6,8,3),np.uint8)
#Crear una imagen de color blanco
img2 = 255*np.ones((6,8,3),np.uint8)

#Establecer 4 píxeles colores en img fondo negro
img1[1, 1] = (50 , 50 , 50)
img1[4, 4] = (200 , 150 ,10)
img1[3, 5] = (75, 100, 255)
img1[2, 3] = (255, 50 , 100)

#Establecer 4 píxeles colores en img fondo blanco
img2[1, 1] = (0 , 255 , 255)
img2[4, 4] = (30 , 50 ,255)
img2[3, 5] = (255, 255, 50)
img2[2, 3] = (150, 250 , 50)

#Mostrar imagen
cv2.imshow('imagen1',img1)
cv2.imshow('imagen2',img2)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

![ones-color](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_250/v1611791463/kipunaEC/pixeles/blancoRGB_pdxi0u.png)
_Fig 8. Imagen BGR inicialmente de color blanco, con cambios de color en píxeles_

![zeros-color](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_250/v1611791464/kipunaEC/pixeles/negroRGB_lr5wsx.png)
_Fig 9. Imagen BGR inicialmente de color negro, con cambios de color en píxeles_

***

## Tipo de dato en numpy.zeros y numpy.ones al crear una imagen

Cuando se crea la matriz para una imagen se espcifica el tipo de dato como `uint8`, en python hay varios [tipos de dato](https://numpy.org/doc/stable/user/basics.types.html) pero no todos funciona para crear imágenes.

El siguiente código muestra tres imágenes creadas con diferentes con diferentes tipos de datos.

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>

1. Importar librerías [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html), [cv2](https://opencv.org/)
2. Crear tres matrices de 3 dimensiones[^4] llenas de unos `1`
 * `uint8` tipo de dato de 8 bits (entero sin signo de 0 a 255), muestra la imagen como es realmente.
 * `uint16` tipo de dato es de 16 bits (enter sin signo de 0 a 65535) los píxeles se dividen por 256, es decir que su rango es desde `[0, 255*256]`.
 * `float32` tipo de dato float de 32 bits, los píxeles se multiplican por `256`
3. Especificar cuatro colores en las mismas posiciones, diferentes imágenes.
 * img[1, 1] = (0 , 255 , 255)
 * img[4, 4] = (30 , 50 ,255)
 * img[3, 5] = (255, 255, 50)
 * img[2, 3] = (150, 250 , 50) 
4. Mostrar las 4 imágenes para comparar

</details>
{::options parse_block_html="false" /} 
 

```python
#Importar librería cv2 y numpy
import cv2
import numpy as np

#Crear una imagen de color blanco uinit8
img1 = 255*np.ones((6,8,3),np.uint8)

#Crear una imagen de color blanco uinit16
img2 = 255*np.ones((6,8,3),np.uint16)

#Crear una imagen de color blanco float32
img3 = 255*np.ones((6,8,3),np.float32)

#Establecer 4 píxeles colores en img1
img1[1, 1] = (0 , 255 , 255)
img1[4, 4] = (30 , 50 ,255)
img1[3, 5] = (255, 255, 50)
img1[2, 3] = (150, 250 , 50)

#Establecer 4 píxeles colores en img2
img2[1, 1] = (0 , 255 , 255)
img2[4, 4] = (30 , 50 ,255)
img2[3, 5] = (255, 255, 50)
img2[2, 3] = (150, 250 , 50)

#Establecer 4 píxeles colores en img3
img3[1, 1] = (0 , 255 , 255)
img3[4, 4] = (30 , 50 ,255)
img3[3, 5] = (255, 255, 50)
img3[2, 3] = (150, 250 , 50)

#Mostrar imagen
cv2.imshow('imagen-uint8',img1)
cv2.imshow('imagen-uint16',img2)
cv2.imshow('imagen-float32',img3)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

![dtype-color](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_350/v1611863857/kipunaEC/pixeles/datatype_myofxb.png)
_Fig 10. Comparación de 3 imágenes BGR con distints tipos de dato_

**Fig 10** mustra como el tipo de dato hace que las imágenes se representen de diferente forma, aunque tenga definidos los mismos colores. Para que se muestren iguales se debe considerar el número de bits que maneja cada tipo de dato y el rango que reresentan [^2] [^3].

### Mostrar la misma imágen con distintos tipos de dato

1. `uint8` muestra la imágen sin modificaciones
2. `uint16` debe ser multiplicado por `256`
3. `float32` debe ser dividido para `256`

```python
#Importar librería cv2 y numpy
import cv2
import numpy as np

#Crear una imagen de color blanco uinit8
img1 = 255*np.ones((6,8,3),np.uint8)

#Crear una imagen de color blanco uinit16
img2 = 255*np.ones((6,8,3),np.uint16)*256

#Crear una imagen de color blanco float32
img3 = 255*np.ones((6,8,3),np.float32)/256

#Establecer 4 píxeles colores en img fondo blanco
img1[1, 1] = (0 , 255 , 255)
img1[4, 4] = (30 , 50 ,255)
img1[3, 5] = (255, 255, 50)
img1[2, 3] = (150, 250 , 50)

img2[1, 1] = (0*256 , 255*256 , 255*256)
img2[4, 4] = (30*256 , 50*256 ,255*256)
img2[3, 5] = (255*256, 255*256, 50*256)
img2[2, 3] = (150*256, 250*256 , 50*256)

img3[1, 1] = (0/256 , 255/256 , 255/256)
img3[4, 4] = (30/256 , 50/256 ,255/256)
img3[3, 5] = (255/256, 255/256, 50/256)
img3[2, 3] = (150/256, 250/256 , 50/256)

#Mostrar imagen
cv2.imshow('imagen-uint8',img1)
cv2.imshow('imagen-uint16',img2)
cv2.imshow('imagen-float32',img3)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

![dtype-color2](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_350/v1611868656/kipunaEC/pixeles/bits2_b5jxdz.png)
_Fig 11. Comparación de 3 imágenes BGR con diferentes tipos de datos, modificados_

***

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/-judWEWZMyY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

***

> Aprendan siempre, aprendan mucho — Mimi

***

## Referencias

[^1]: Joel. (28 de Febrero del 2019). [Publicado en {lwp}]. *Crear un imagen con cada pixel de un color* [https://www.lawebdelprogramador.com/codigo/Python/5175-Crear-un-imagen-con-cada-pixel-de-un-color.html](https://www.lawebdelprogramador.com/codigo/Python/5175-Crear-un-imagen-con-cada-pixel-de-un-color.html)

[^2]: OpenCV. imshow [https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html#imshow](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html#imshow)

[^3]: univerio. (20 de Mayo del 2014). [Publicación en un foro online]. *why datatype has to be 'uint8' in Opencv python wrapper*. Mensaje publicado en [https://stackoverflow.com/questions/23749968/why-datatype-has-to-be-uint8-in-opencv-python-wrapper](https://stackoverflow.com/questions/23749968/why-datatype-has-to-be-uint8-in-opencv-python-wrapper)

[^4]: Web Development Labs. (4 de septiembre del 2020). [Publicación en un foro online]. *3-dimensional array in numpy* .[https://stackoverflow.com/questions/22981845/3-dimensional-array-in-numpy](https://stackoverflow.com/questions/22981845/3-dimensional-array-in-numpy)


