---
title: Crear una imagen BGR openCV-python
date: 2021-01-21 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, texto, imagen]   
math: true
image: https://res.cloudinary.com/dxh1bpaim/image/upload/v1611791463/kipunaEC/pixeles/blancoRGB_pdxi0u.png
---
## Crear una imagen en openCV - python
Escribo este post porque inicialmente quería dibujar formas y texto en openCV, una de las maneras de hacerlo es [dibujar y escribir sobre una imagen](../Añadir-texto-a-una-imagen-python-openCV/) **¡realmente fue sencillo!**, pero luego surguió la interrogante, que tal que no quiero usar una imagen como tal (es decir leerla con `imread`) y quiero generar yo misma el fondo (crear una imagen negra, blanca, gris, etc) para escribir y dibujar las formas. En esa busqueda enconté esta línea de codigo:

 `img = np.ones((100,100,3),np.uint8)` [^1] 
 
 Usada para crear un área de `100 x 100`que representará una imagen **!ok, yo estaba de acuerdo!**, pero que significa el `3` y `dtype=np.uint8` en esa expesión? 

* El `3` significa los canales que tiene la imagen en este caso son `B G R`. 

* `dtype=np.uint8` significa el tipo de dato de cada píxel

Bueno, para profundizar voy a empezar detallando como se representan las imágenes digitales en python y openCV.

## Imagen digital 

Una computadora ve las imágenes como cuadrículas con números, cada una de estas cadriculas se llama [píxel](../Pixeles-openCV-Python/), una imagen digital esta representada por la combinación de píxeles formando filas y columnas **Fig1** y **Fig2**.  

![píxelesGRIS](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_493,w_948/v1611690433/kipunaEC/pixeles/alpaca3_t5rtmu.png "píxeles GRIS"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 1. píxeles en una imagen en escala de grises</p>
</center>


![píxelesBGR](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_513,w_1021/v1611688064/kipunaEC/pixeles/alpaca1_esht7l.png "píxeles BGR"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 2. píxeles en una imagen BGR</p>
</center>

### **¿Cuál es la diferencia entre Fig1 (escala de grises) y Fig2 (BGR )?**

La diferencia entre estas dos imágenes esta en la cantidad de **canales**
* En **Fig1** cada cuadrícula (píxel) tiene `1` número entre 0 a 255 y representa un canal. 
* En **Fig2** cada cuadrícula (píxel) tiene `3` números entre 0 a 255 y representan tres canales `B`, `G`, `R`.

Ahora, considerando que una imagen es una matriz de valores numerícos y que la combinación de los `3` canales `BGR` hacen que una imagen tome color, empieza a tener sentido la línea de código que mencioné al inicio `img = np.zeros((500,500,3),np.uint8)`

## ¿Cómo funciona **np.ones** y **np.zeros** para crear una imagen?

[ones](https://numpy.org/doc/stable/reference/generated/numpy.ones.html) y [zeros](https://numpy.org/doc/stable/reference/generated/numpy.zeros.html) son funcines de la librería [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html) para python, craen matrices  llenas de unos `1` o ceros `0` respectivamente.
Para crear una imagen en openCV recibe como parámetros, las dimensiones de la imagen `shape` y el tipo de dato de cada píxel `dtye`

```python
numpy.ones(shape, dtype)
numpy.zeros(shape, dtype)
```

1. `shape` puede ser un entero o una tupla de enteros
2. `dtpe` establece el tipo de dato del arreglo que se va a crear, por defecto es `numpy.float64` *Más adelante registro como afecta el tipo de dato a la construcción de una imagen*

## Crear una imagen en escala de grises

Una imagenen debe ser una representación numérica en forma de matriz como **Fig 3** y **Fig 4**.

![zeros](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_187,w_350/v1611701744/kipunaEC/pixeles/zeros_lit9t2.png "zeros"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 3. Matriz 6x8 llena de ceros </p>
</center>

![ones](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_187,w_350/v1611701744/kipunaEC/pixeles/ones_h8sg1z.png "ones"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 4. Matriz 6x8 llena de unos </p>
</center>

En el siguiente código genero dos imágenes de color negro con las funciones `zeros` y `ones`, el color de fondo de **Fig 3** y **Fig 4** son similares porque los valores en los píxeles son consecutivos `0` y `1`, para notar cambios en los colores los valores deben variar entre `0` a `255`

1. Importar librerías [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html), [cv2](https://opencv.org/)
2. Crear la matriz de `3`dimensiones
 * `np.zeros((6,8,1)` imagen `alto = 6`, `ancho = 8` y en cada posición estará `1` valor. Toda la matriz esta llena de `ceros`.
 * `255*np.ones((6,8,1)` imagen `alto = 6`, `ancho = 8` y en cada posición estará `1` valor. Toda la matriz esta llena de `255`.

```python
#Importar librería cv2
import cv2
import numpy as np

img1 = np.zeros((6,8,1),np.uint8)
img2 = np.ones((6,8,1),np.uint8)

#Mostrar imagenes
cv2.imshow('imagen-zeros',img1)
cv2.imshow('imagen-ones',img2)
```

### Cambiar de color (tonalidad) a los píxeles en escala de grises

El color de un píxel será negro mientras sea cercano a `0` y tomará tonalidades de color blanco mientras mas sea cercano a `255`, el siguiente código muestra como se agrega valores a píxeles específicos (esta hecho con `zeros`, pero tambien funciona con `ones`) 

```python
#Importar librería cv2 y numpy
import cv2
import numpy as np

img1 = np.zeros((6,8,1),np.uint8)

#colocar valores en píxeles especìficos
img1[1,1] = 50
img1[4,4] = 200
img1[3,5] = 75
img1[2,3] = 255

#Guardo la imagen
cv2.imwrite('Img-zeros.jpg', img1)
```

![zeros](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_187,w_350/v1611771588/kipunaEC/pixeles/tonalidadgris_kfylxc.png "zeros"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 5. imagen de 6x8 en escala de grises, algunos píxeles fueron cambiados de tono</p>
</center>

## Crear una imagen BRG

Una imagen BGR debe ser la representacón numeríca de una matriz, a diferencia de la escala de grises en cada píxel existirá tres valores entre `0` y `255`  

![3d](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_287,w_418/v1611697512/kipunaEC/pixeles/RGB2_hazv0n.png "3d"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 6. representación intuitiva de una umagen BGR </p>
</center>

El siguiente código genera una imagen `BGR`, creando el arreglo numérico con las funciones `zeros` y `ones`.
1. Importar librerías [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html), [cv2](https://opencv.org/)
2. Crear la matriz de `3`dimensiones
 * `np.zeros((6,8,3)` imagen `alto = 6`, `ancho = 8` y `3` canales `B G R`. Toda la matriz de `3` dimensiones esta llena de `ceros`, por lo tanto la imagen es de color negro.
 * `255*np.ones((6,8,3)` imagen `alto = 6`, `ancho = 8` y `3` canales `B G R`. Toda la matriz de `3`dimensiones esta llena de `255`, por lo tanto la imagen será de color blanco. 

```python
#Importar librería cv2 y numpy
import cv2
import numpy as np

#Crear una imagen de color negro
img1 = np.zeros((6,8,3),np.uint8)
#Crear una imagen de color blanco
img2 = 255*np.ones((6,88-bit unsigned,3),np.uint8)

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
**Fig 7** y **Fig 8** es el resultado del código anterior, y **Fig 9** y **Fig 10** son las mismas imágenes respectivamente vizualizadas con un acercamiento en openCV.

![ones](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_69,w_90/v1611851344/kipunaEC/pixeles/pixelescolorBGR_s8ssgp.png "ones"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 7. Imagen BGR, arreglo numérico creado con ones</p>
</center>

![ones](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_68,w_89/v1611852129/kipunaEC/pixeles/colornegro_flqixu.png "ones"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 8. Imagen BGR, arreglo numérico creado con zeros</p>
</center>

![ones](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_275,w_350/v1611791463/kipunaEC/pixeles/blancoRGB_pdxi0u.png "ones"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 9. Imagen BGR inicialmente de color blanco, con cambios de color en píxeles</p>
</center>

![zeros](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_275,w_350/v1611791464/kipunaEC/pixeles/negroRGB_lr5wsx.png "zeros"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 10. Imagen BGR inicialmente de color negro, con cambios de color en píxeles</p>
</center>


## Tipo de dato en numpy.zeros y numpy.ones al crear una imagen

Al crear la matriz para una imagen se espcifiva el tipo de dato como `uint8`, en python hay varios [tipos de dato](https://numpy.org/doc/stable/user/basics.types.html) pero no todos funciona para crear imagines.




En el siguiente código muestro tres imágenes con diferentes En este ejmplo hago pruebas con `3`tipos de datos [^2]
1. Importar librerías [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html), [cv2](https://opencv.org/)
2. Crear tres matrices de 3 dimensiones llenas de unos `1`
 * `uint8` tipo de dato de `8` bits (entero sin signo de 0 a 255), muestra la imagen como es
 * `uint16` si el tipo de dato es de 16 bits (enter sin signo de 0 a 65535) los píxeles se dividen por `256`, es decir que su rango es desde `[0, 255*256]`.
 * `float32` si el tipo de dato es float de 32 bits los píxeles se multiplican por `256`
3. Específicar cuatro colores en las mismas posiciones, diferentes imágenes
 * img[1, 1] = (0 , 255 , 255)
 * img[4, 4] = (30 , 50 ,255)
 * img[3, 5] = (255, 255, 50)
 * img[2, 3] = (150, 250 , 50) 
4. Mostrar las 4 imágenes para comparar

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

![dtype](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_451,w_367/v1611863857/kipunaEC/pixeles/datatype_myofxb.png "dtype"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 11. Imagen BGR inicialmente de color negro, con cambios de color en píxeles</p>
</center>

**Fig 11** mustra como el tipo de dato hace que se  muestre de distintas formas las imágenes. Para que todas se muestre iguales se debe consideraa el núero de bots que maneja cada tipi de dato y como onflute en la imágen [^2] [^3].

1. `uint8` muestra la imágen sin modificacines
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

![dtype](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_450,w_369/v1611868656/kipunaEC/pixeles/bits2_b5jxdz.png "dtype"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 11. Imagen BGR inicialmente de color negro, con cambios de color en píxeles</p>
</center>

## Referencias

[^1]: Joel. (28 de Febrero del 2019). [Publicado en {lwp}]. *Crear un imagen con cada pixel de un color* [https://www.lawebdelprogramador.com/codigo/Python/5175-Crear-un-imagen-con-cada-pixel-de-un-color.html](https://www.lawebdelprogramador.com/codigo/Python/5175-Crear-un-imagen-con-cada-pixel-de-un-color.html)

[^2]: OpenCV. imshow [https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html#imshow](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html#imshow)

[^3]: univerio. (20 de Mayo del 2014). [Publicación en un foro online]. *why datatype has to be 'uint8' in Opencv python wrapper*. Mensaje publicado en [https://stackoverflow.com/questions/23749968/why-datatype-has-to-be-uint8-in-opencv-python-wrapper](https://stackoverflow.com/questions/23749968/why-datatype-has-to-be-uint8-in-opencv-python-wrapper)

[https://stackoverflow.com/questions/22981845/3-dimensional-array-in-numpy](https://stackoverflow.com/questions/22981845/3-dimensional-array-in-numpy)


