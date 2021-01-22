---
title: Cambio de espacios de color python - openCV 
date: 2021-01-17 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, cvtColor, color, rgb, gris, gray]
---

## Espacios de color

Un [espacio de color](https://es.wikipedia.org/wiki/Espacio_de_color) es una gama de colores que permite representar una imagen. 
En este post registro los cambios de espacios partiendo desde el [modelo de color RGB](https://es.wikipedia.org/wiki/Modelo_de_colores) hasta espacios de color como [gris](#escala-de-grises---color_rgb2gray), [RGBA](#color_rgb2rgba), [BGRA](#color_rgb2bgra), [XYZ](#color_rgb2xyz), [YCrCb](#color_rgb2ycrcb), [HSV](#color_rgb2hsv), [Lab](#color_rgb2lab), [Luv](#color_rgb2luv), [HLS](#color_rgb2hls), [YUV](#color_rgb2yuv)  en python y openCV usando la función `cvtColor`.

![imagen-original](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_225,w_200/v1611284387/kipunaEC/espacios-color/espacios_vxo3zs.gif "imagen-RGB"){:.thumbnail.bordered, width= 5 }

## Cambio de espacios de color - cvtColor 
[cvtColor](https://docs.opencv.org/3.4/db/d64/tutorial_js_colorspaces.html) es una función de openCV que convierte imágenes de un espacio de color a otro.
En openCV hay más de 150 espacios disponibles [código de la conversión del espacio de color](https://docs.opencv.org/3.4/d8/d01/group__imgproc__color__conversions.html#ga4e0972be5de079fed4e3a10e24ef5ef0).

Fig1 muestra la imagen que va a cambiar de espacios de color, originalmente es `RGB` con  `ancho = 594, alto = 567` y `3 canales`. 

![imagen-original](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_375,w_300/v1611196936/kipunaEC/espacios-color/ungatito1-rgb-min_ztpbjm.jpg "imagen-RGB"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 1. Imagen RGB original, un gatito</p>
</center>

## Escala de grises - COLOR_RGB2GRAY

![imagen-original](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_377,w_300/v1611196936/kipunaEC/espacios-color/rbg-gris-min_kytfwe.jpg "imagen-gris"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 2. un gatito GRIS (conversión RGB -> GRIS)</p>
</center>

En siguiente código python openCV generó Fig2. 
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

## COLOR_RGB2RGBA

[RGBA](https://es.wikipedia.org/wiki/Espacio_de_color_RGBA) son la siglas para red, green, blue, alpha. El canal *alpha* indica la opacidad de cada pixel

![RGBA](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_366,w_350/v1611199764/kipunaEC/espacios-color/RGB-RGBA-min_tegbht.jpg "RGBA"){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 3. un gatito RGBA (conversión RGB -> RGBA)</p>
</center>
En esta conversión Fig3. no se aprecia modificaciones en la imagen, pero el [espacio de color RGBA](https://es.wikipedia.org/wiki/Espacio_de_color_RGBA) añade un canal (alpha), ahora son `4` como se ve a continuación en la terminal.
```terminal
alto, alto, canales = (594, 567, 4)
```
## COLOR_RGB2BGRA 

![BGRA](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_366,w_350/v1611199763/kipunaEC/espacios-color/RGB-GBRA-min_yvhgl4.jpg "RGB-BGRA "){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 4. un gatito BGRA  (conversión RGB -> BGRA )</p>
</center>

```terminal
alto, alto, canales = (594, 567, 4)
```

## COLOR_RGB2XYZ

![BGRA](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_366,w_350/v1611199764/kipunaEC/espacios-color/RGB-RGBA-min_tegbht.jpg "RGB-XYZ "){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 4. un gatito BGRA  (conversión RGB -> BGRA )</p>
</center>

```terminal
alto, alto, canales = (594, 567, 3)
```

## COLOR_RGB2YCrCb 

![YCrCb ](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_366,w_350/v1611202577/kipunaEC/espacios-color/RGB-YCrCb_-min_voozb1.jpg "RGB-YCrCb  "){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 5. un gatito YCrCb  (conversión RGB -> YCrCb  )</p>
</center>

```terminal
alto, alto, canales = (594, 567, 3)
```
## COLOR_RGB2HSV

![HSV ](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_366,w_350/v1611202953/kipunaEC/espacios-color/RGB-HSV_-min_djfgnu.jpg "RGB-HSV  "){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 6. un gatito HSV  (conversión RGB -> HSV  )</p>
</center>

```terminal
alto, alto, canales = (594, 567, 3)
```

## COLOR_RGB2Lab 

![Lab](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_384,w_366/v1611203193/kipunaEC/espacios-color/RGB-Lab-min_ybzxab.jpg "RGB-Lab "){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 7. un gatito Lab  (conversión RGB -> Lab  )</p>
</center>

```terminal
alto, alto, canales = (594, 567, 3)
```

## COLOR_RGB2Luv

![Luv](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_418,w_400/v1611203435/kipunaEC/espacios-color/RGB-Luv-min_bybbhb.jpg "RGB-Luv "){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 8. un gatito Luv  (conversión RGB -> Luv  )</p>
</center>

```terminal
alto, alto, canales = (594, 567, 3)
```
## COLOR_RGB2HLS

![HLS](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_418,w_400/v1611203678/kipunaEC/espacios-color/RGB-HLS-min_cynt4n.jpg "RGB-HLS "){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 9. un gatito HLS  (conversión RGB -> HLS  )</p>
</center>

```terminal
alto, alto, canales = (594, 567, 3)
```

## COLOR_RGB2YUV

![YUV](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_418,w_400/v1611203889/kipunaEC/espacios-color/RGB-YUV-min_uldpuz.jpg "RGB-YUV "){:.thumbnail.bordered, width= 5 }
<center>
<p style="color: rgb(199,207,210);"> Fig 10. un gatito YUV  (conversión RGB -> YUV  )</p>
</center>

```terminal
alto, alto, canales = (594, 567, 3)
```


Los espacios de color que registro en este post parten del `RGB` (porque mi imagen original Fig1 estaba en el espacio RGB), también se puede invertir los espacios de color. 



## Referencias

1. Blog del fotógrafo, *¿Qué es y para que sirve el espacio de color?*. Publicado en: [https://www.blogdelfotografo.com/espacio-color/](https://www.blogdelfotografo.com/espacio-color/)
2. OpenCV. *Changing Colorspaces* [https://docs.opencv.org/3.4/db/d64/tutorial_js_colorspaces.html](https://docs.opencv.org/3.4/db/d64/tutorial_js_colorspaces.html)
