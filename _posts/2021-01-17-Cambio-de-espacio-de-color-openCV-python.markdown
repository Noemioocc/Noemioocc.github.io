---
title: Cambio de espacios de color openCV - python
date: 2021-01-17 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, cvtColor, color, rgb, gris, gray]
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612471827/kipunaEC/espacios-color/formas_aywvcd.gif
---

***

## Espacios de color

Un [espacio de color](https://es.wikipedia.org/wiki/Espacio_de_color) es una gama de colores que permite representar una imagen. 
Este post registra los cambios de espacios partiendo desde el [modelo de color BGR](https://learnopencv.com/why-does-opencv-use-bgr-color-format/) hasta espacios de color como [gris](#escala-de-grises---color_rgb2gray), [BGRA](#color_bgr2bgra), [YCrCb ](#color_bgr2ycrcb), [XYZ](#color_bgr2xyz), [HSV](#color_bgr2hsv), [Lab](#color_bgr2lab), [Luv](#color_bgr2luv), [HLS](#color_bgr2hls), [YUV](#color_bgr2yuv)  en python y openCV usando la función `cvtColor`.

***

## Cambio de espacios de color - cvtColor 
[cvtColor](https://docs.opencv.org/3.4/db/d64/tutorial_js_colorspaces.html) es una función de openCV que convierte imágenes de un espacio de color a otro.
En openCV hay más de 150 espacios disponibles [código de la conversión del espacio de color](https://docs.opencv.org/3.4/d8/d01/group__imgproc__color__conversions.html#ga4e0972be5de079fed4e3a10e24ef5ef0).

**Fig 1** muestra la imagen que va a cambiar de espacios de color, originalmente es `RGB` con  `ancho = 594, alto = 567` y `3 canales`. 

![imagen-original](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472808/kipunaEC/espacios-color/gato_venlup.jpg)
_Fig 1. Imagen BGR original, un gatito_

***

## Escala de grises - COLOR_RGB2GRAY

![imagen-gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472782/kipunaEC/espacios-color/COLOR_BGR2GRAY_emtg6m.jpg
)
_Fig 2. Un gatito GRIS (conversión RGB -> GRIS)_

En siguiente código python openCV generó **Fig 2**. 
1. [numpy](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html), [cv2](https://opencv.org/) importar librerías 
2. [imread](https://docs.opencv.org/master/d4/da8/group__imgcodecs.html#ga288b8b3da0892bd651fce07b3bbd3a56), leer imagen RGB `img` *gato.jpg* 
3. `ìmg2` variable usada para almacenar la conversión de espacio de color de `img`.
 * `cvtColor` tiene dos argumentos `img` y `COLOR_RGB2GRAY`
 * `img`imagenn original sin cambios en el espacio de color
 * `COLOR_RGB2GRAY` [código de la conversión del espacio de color](https://docs.opencv.org/3.4/d8/d01/group__imgproc__color__conversions.html#ga4e0972be5de079fed4e3a10e24ef5ef0) en este caso la conversión es de `RGB` a `Gris`
5. `alto, ancho, canales`, imprimir en la consola con [print()](https://docs.python.org/3/whatsnew/3.0.html).
 * `img2.shape` características de `img2`, dimensiones y canales.
6. `cv2.imshow('Un gatito GRIS',img2)`, mostrar `img2` en una ventana 

```python
import numpy as np
import cv2

#Leer una imagen
img = cv2.imread('gato.jpg')

#Cambiar el espacio de color en img2
img2 = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY )

#Imprimo características de la imagen en su nuevo espacio de color
# alto, ancho y canales
print("alto, alto, canales = "+ str(img2.shape))

#Muestro la imagen
cv2.imshow('Un gatito GRIS',img2)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
En la conversión a escala de grises se imprime el alto y ancho, sin canales.
```terminal
alto, alto, canales = (594, 567)
```
A continuación se modifica `COLOR_RGB2GRAY` por otra [ conversión del espacio de color](https://docs.opencv.org/3.4/d8/d01/group__imgproc__color__conversions.html#ga4e0972be5de079fed4e3a10e24ef5ef0), y se muestra los resultados (imagen e impresión de datos en la terminal)

***

## COLOR_BGR2BGRA

BGRA son la siglas para red, green, blue, alpha. El canal *alpha* indica la opacidad de cada pixel.

![imagen-BGRA](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472785/kipunaEC/espacios-color/COLOR_BGR2BGRA_iqi5x4.jpg)
_Fig 3. Un gatito BGR (conversión BGR -> BGRA)_

En esta conversión **Fig 3** no se aprecia modificaciones en la imagen, pero `BGR` añade un canal (alpha), ahora son `4` como se ve a continuación en la terminal.

```terminal
alto, alto, canales = (594, 567, 4)
```

***

## COLOR_BGR2RGB

![imagen-RGB](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472763/kipunaEC/espacios-color/COLOR_BGR2RGB_wsedlj.jpg)
_Fig 4. Un gatito RGB (conversión BGR -> RGB)_

```terminal
alto, alto, canales = (594, 567, 3)
```

***

## COLOR_BGR2RGBA

![imagen-RGBA](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472770/kipunaEC/espacios-color/COLOR_BGR2RGBA_j6qb4h.jpg)
_Fig 5. Un gatito BGRA (conversión BGR -> RGBA)_

```terminal
alto, alto, canales = (594, 567, 4)
```

***

## COLOR_BGR2YCrCb 

![imagen-YCrCb](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472759/kipunaEC/espacios-color/COLOR_BGR2YCrCb_q63glu.jpg)
_Fig 6. Un gatito YCrCb (conversión BGR -> YCrCb)_

```terminal
alto, alto, canales = (594, 567, 3)
```

***

## COLOR_BGR2HSV

![imagen-HSV](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472774/kipunaEC/espacios-color/COLOR_BGR2HSV_vworgv.jpg)
_Fig 7. Un gatito HSV (conversión BGR -> HSV)_

```terminal
alto, alto, canales = (594, 567, 3)
```

***

## COLOR_BGR2HSV_FULL

![imagen-HSVFULL](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472783/kipunaEC/espacios-color/COLOR_BGR2HSV_FULL_pqln3n.jpg)
_Fig 8. Un gatito HSV_FULL (conversión BGR -> HSV_FULL)_

```terminal
alto, alto, canales = (594, 567, 3)
```

***

## COLOR_BGR2Lab 

![imagen-Lab](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472765/kipunaEC/espacios-color/COLOR_BGR2Lab_hwjvez.jpg)
_Fig 9. Un gatito Lab (conversión BGR -> Lab)_

```terminal
alto, alto, canales = (594, 567, 3)
```

***

## COLOR_BGR2Luv

![imagen-Luv](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472758/kipunaEC/espacios-color/COLOR_BGR2Luv_eblgvk.jpg)
_Fig 9. Un gatito Luv (conversión BGR -> Luv)_

```terminal
alto, alto, canales = (594, 567, 3)
```

***

## COLOR_BGR2HLS

![imagen-HLS](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472788/kipunaEC/espacios-color/COLOR_BGR2HLS_oh7ovo.jpg)
_Fig 10. Un gatito HLS (conversión BGR -> HLS)_

```terminal
alto, alto, canales = (594, 567, 3)
```

***

## COLOR_BGR2HLS_FULL

![imagen-HLS_FULL](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472781/kipunaEC/espacios-color/COLOR_BGR2HLS_FULL_wbhor9.jpg)
_Fig 11. Un gatito HLS_FULL (conversión BGR -> HLS_FULL)_

```terminal
alto, alto, canales = (594, 567, 3)
```

***

## COLOR_BGR2YUV 

![imagen-YUV ](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472761/kipunaEC/espacios-color/COLOR_BGR2YUV_lyhhom.jpg)
_Fig 12. Un gatito HLS_YUV  (conversión BGR -> YUV )_

```terminal
alto, alto, canales = (594, 567, 3)
```

## COLOR_BGR2XYZ

![imagen-XYZ ](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1612472771/kipunaEC/espacios-color/COLOR_BGR2XYZ_yw4g1w.jpg)
_Fig 12. Un gatito XYZ  (conversión BGR -> XYZ )_

```terminal
alto, alto, canales = (594, 567, 3)
```
***

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

1. Blog del fotógrafo, *¿Qué es y para que sirve el espacio de color?*. Publicado en: [https://www.blogdelfotografo.com/espacio-color/](https://www.blogdelfotografo.com/espacio-color/)
2. OpenCV. *Changing Colorspaces* [https://docs.opencv.org/3.4/db/d64/tutorial_js_colorspaces.html](https://docs.opencv.org/3.4/db/d64/tutorial_js_colorspaces.html)

3. alexander334. (5 de enero del 2017). *RGB vs. BGR* . [https://answers.opencv.org/question/31437/rgb-vs-bgr/](https://answers.opencv.org/question/31437/rgb-vs-bgr/)

4. Vladislav Vinogradov. (27 de febrero del 2013). *Images RGB and BGR*. [https://answers.opencv.org/question/8132/images-rgb-and-bgr/](https://answers.opencv.org/question/8132/images-rgb-and-bgr/)
