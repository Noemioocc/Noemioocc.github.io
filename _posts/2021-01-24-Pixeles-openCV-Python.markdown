---
title: Píxeles en openCV python
date: 2021-01-21 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, texto, imagen]   
math: true
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1612302798/kipunaEC/pixeles/portada-pixel_isrv4e.jpg
redirect_to: https://kipunaec.com/pixeles-en-opencv-python/
---

***

## Píxeles

Un [píxel](https://es.wikipedia.org/wiki/P%C3%ADxel) es la unidad más pequeña de una imagen digital. **Fig1** muestra una porción ampliada de una imagen, cada cuadro respresenta un píxel y tiene un [color](https://htmlcolorcodes.com/es/) específico.

![pixel-imagen](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_240,w_400/v1612304704/kipunaEC/pixeles/pixel100_zlcswt.png)
_Fig 1. Píxeles en una imagen_

 ***

## Acceder al valor específico de un píxel BGR openCV python

Como se menciona en el post [crear una imagen BGR](../Crear-una-imagen-BGR-openCV-Python/), una computadora ve una imagen digital como un arreglo de números. **Fig2** muestra una imagen que representa 9 píxeles de **alto** (fila) y 9 píxeles de **ancho** (columnas), y cada uno de estos espacios contiene `3`valores entre `0` y `255`: 
* `B` Blue, `G` Green, `R` Red.

*Nota: En openCV por defecto, la representación  de los colores es en el orden BGR*

![pixeles-representación](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_100/v1612305836/kipunaEC/pixeles/pixel2_lzyu0x.png)
_Fig 2. Representación de 9x9 píxeles_

El siguiente código permite hallar los  valores `BGR` que representan el color de la esquina superior izquierda `[0,0]` y  de la esquina inferior derecha `[8,8]`.

*Nota: Anteriormente se dijo que la imagen es de 9x9 píxeles, pero la posición inicial de un arreglo en python es `0` y se considera hasta la posición `[8,8]`, en este ejemplo la posición `[9,9]` no existe*.

```python
#Importar librería cv2
import cv2

#Leer imagen
img = cv2.imread('pixeles.jpg')

#Conocer el valor del pixel (0 ,0) y (8,8)
print("Color posición 0,0: " + str(img[0,0]) )
print("Color posición 8,8: " + str(img[8,8]) )

#Mostrar imagen
cv2.imshow('imagen',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
```terminal 
Color posición 0,0: [  8  80 164]
Color posición 8,8: [ 47 196 253]
```

***

## Acceder al valor de todos los píxeles en una imagen BGR openCV python

**Fig 3** es una representación intuitiva de como se ubican los 3 valores `B G R` en una imagen. 

![numerica-representación](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612307975/kipunaEC/pixeles/1_ujkchs.jpg)
_Fig 3. Representación numérica intuitiva de 81 colores B G R_

Considerando que **Fig2** representa `81` píxeles, a continuación se obtiene los valore `BGR`de cada uno, con un bucle [for](https://docs.python.org/3/tutorial/controlflow.html#for-statements) para leer las filas y las columnas.

```python
#Importar librería cv2
import cv2

#Leer imagen
img = cv2.imread('pixeles1.jpg')

#Analiza 81 pixeles
for fila in range (9):
    for columna in range (9):
        print("Color", "fila:", + fila, "columna", + columna, "=", str(img[fila,columna]))
```

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Resultado del código en la **terminal**. **Clic para desplegar** 
</summary>

```terminal
Color fila: 0 columna 0 = [  8  80 164]
Color fila: 0 columna 1 = [ 12  85 171]
Color fila: 0 columna 2 = [ 12  89 176]
Color fila: 0 columna 3 = [ 14  96 185]
Color fila: 0 columna 4 = [ 15 103 193]
Color fila: 0 columna 5 = [ 16 109 200]
Color fila: 0 columna 6 = [ 14 113 205]
Color fila: 0 columna 7 = [ 12 115 208]
Color fila: 0 columna 8 = [ 12 116 209]
Color fila: 1 columna 0 = [  8  80 164]
Color fila: 1 columna 1 = [  5  81 164]
Color fila: 1 columna 2 = [  6  86 171]
Color fila: 1 columna 3 = [  8  93 179]
Color fila: 1 columna 4 = [  8  98 186]
Color fila: 1 columna 5 = [  7 104 192]
Color fila: 1 columna 6 = [  6 108 197]
Color fila: 1 columna 7 = [  9 114 205]
Color fila: 1 columna 8 = [ 11 118 209]
Color fila: 2 columna 0 = [  4  78 160]
Color fila: 2 columna 1 = [  0  79 160]
Color fila: 2 columna 2 = [  3  85 167]
Color fila: 2 columna 3 = [  2  93 174]
Color fila: 2 columna 4 = [  0  96 179]
Color fila: 2 columna 5 = [  0  99 185]
Color fila: 2 columna 6 = [  0 105 192]
Color fila: 2 columna 7 = [  7 116 202]
Color fila: 2 columna 8 = [ 13 123 211]
Color fila: 3 columna 0 = [  0  74 151]
Color fila: 3 columna 1 = [  0  80 158]
Color fila: 3 columna 2 = [  2  90 167]
Color fila: 3 columna 3 = [  6  99 178]
Color fila: 3 columna 4 = [  2 103 182]
Color fila: 3 columna 5 = [  0 104 185]
Color fila: 3 columna 6 = [  0 110 192]
Color fila: 3 columna 7 = [  9 123 207]
Color fila: 3 columna 8 = [ 16 134 217]
Color fila: 4 columna 0 = [  0  81 156]
Color fila: 4 columna 1 = [  2  89 163]
Color fila: 4 columna 2 = [  8 102 175]
Color fila: 4 columna 3 = [ 15 114 188]
Color fila: 4 columna 4 = [ 12 119 193]
Color fila: 4 columna 5 = [  9 121 197]
Color fila: 4 columna 6 = [ 10 128 205]
Color fila: 4 columna 7 = [ 18 139 218]
Color fila: 4 columna 8 = [ 26 150 228]
Color fila: 5 columna 0 = [  9  97 167]
Color fila: 5 columna 1 = [ 17 110 179]
Color fila: 5 columna 2 = [ 24 122 192]
Color fila: 5 columna 3 = [ 32 136 207]
Color fila: 5 columna 4 = [ 31 143 213]
Color fila: 5 columna 5 = [ 26 147 217]
Color fila: 5 columna 6 = [ 28 154 225]
Color fila: 5 columna 7 = [ 33 162 235]
Color fila: 5 columna 8 = [ 37 168 241]
Color fila: 6 columna 0 = [ 24 118 184]
Color fila: 6 columna 1 = [ 43 140 206]
Color fila: 6 columna 2 = [ 48 152 217]
Color fila: 6 columna 3 = [ 52 164 230]
Color fila: 6 columna 4 = [ 52 169 236]
Color fila: 6 columna 5 = [ 48 173 241]
Color fila: 6 columna 6 = [ 48 179 246]
Color fila: 6 columna 7 = [ 47 183 249]
Color fila: 6 columna 8 = [ 44 184 250]
Color fila: 7 columna 0 = [ 51 149 213]
Color fila: 7 columna 1 = [ 64 167 230]
Color fila: 7 columna 2 = [ 68 177 239]
Color fila: 7 columna 3 = [ 69 186 247]
Color fila: 7 columna 4 = [ 65 190 251]
Color fila: 7 columna 5 = [ 61 192 255]
Color fila: 7 columna 6 = [ 58 195 255]
Color fila: 7 columna 7 = [ 53 196 255]
Color fila: 7 columna 8 = [ 48 194 254]
Color fila: 8 columna 0 = [ 69 170 232]
Color fila: 8 columna 1 = [ 81 187 248]
Color fila: 8 columna 2 = [ 81 193 253]
Color fila: 8 columna 3 = [ 77 197 255]
Color fila: 8 columna 4 = [ 70 198 255]
Color fila: 8 columna 5 = [ 65 199 255]
Color fila: 8 columna 6 = [ 61 201 255]
Color fila: 8 columna 7 = [ 54 200 255]
Color fila: 8 columna 8 = [ 47 196 253]

```
</details>
{::options parse_block_html="false" /}

*** 

## Acceder al valor numérico de todos los píxeles en una imagen en escala de grises openCV python

La [escala de grises](https://es.wikipedia.org/wiki/Escala_de_grises) posee un solo valor (1 canal) entre `0` y `255` como se ve en **Fig 4**. A diferenia de BGR  que posee tres valores en cada píxel. 

![numerica-representación-gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612307972/kipunaEC/pixeles/2_ns3zbe.jpg)
_Fig 4. Representación numérica intuitiva de 81 píxeles en esacala de grises_

El siguiente código muestra como se extrae los valores de todos los píxeles. 

```python
#Importar librería cv2
import cv2

#Leer imagen
img = cv2.imread('pixeles.jpg')
#Cambiar img a escala de grises
img2 = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

#Analiza 81 pixeles grises
for fila in range (9):
    for columna in range (9):
        print("Color", "fila:", + fila, "columna", + columna, "=", str(img2[fila,columna]))

#Mostrar imagen
cv2.imshow('imagenGris',img2)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
{::options parse_block_html="true" /}

<details>
<summary markdown='span'>  Resultado del código en la **terminal**. **Clic para desplegar**
</summary>

```terminal
Color fila: 0 columna 0 = 68
Color fila: 0 columna 1 = 73
Color fila: 0 columna 2 = 76
Color fila: 0 columna 3 = 82
Color fila: 0 columna 4 = 87
Color fila: 0 columna 5 = 92
Color fila: 0 columna 6 = 94
Color fila: 0 columna 7 = 95
Color fila: 0 columna 8 = 96
Color fila: 1 columna 0 = 68
Color fila: 1 columna 1 = 68
Color fila: 1 columna 2 = 72
Color fila: 1 columna 3 = 77
Color fila: 1 columna 4 = 81
Color fila: 1 columna 5 = 85
Color fila: 1 columna 6 = 88
Color fila: 1 columna 7 = 93
Color fila: 1 columna 8 = 96
Color fila: 2 columna 0 = 65
Color fila: 2 columna 1 = 65
Color fila: 2 columna 2 = 70
Color fila: 2 columna 3 = 75
Color fila: 2 columna 4 = 77
Color fila: 2 columna 5 = 79
Color fila: 2 columna 6 = 84
Color fila: 2 columna 7 = 93
Color fila: 2 columna 8 = 100
Color fila: 3 columna 0 = 61
Color fila: 3 columna 1 = 65
Color fila: 3 columna 2 = 72
Color fila: 3 columna 3 = 80
Color fila: 3 columna 4 = 82
Color fila: 3 columna 5 = 82
Color fila: 3 columna 6 = 86
Color fila: 3 columna 7 = 98
Color fila: 3 columna 8 = 108
Color fila: 4 columna 0 = 65
Color fila: 4 columna 1 = 71
Color fila: 4 columna 2 = 82
Color fila: 4 columna 3 = 93
Color fila: 4 columna 4 = 95
Color fila: 4 columna 5 = 96
Color fila: 4 columna 6 = 101
Color fila: 4 columna 7 = 112
Color fila: 4 columna 8 = 122
Color fila: 5 columna 0 = 79
Color fila: 5 columna 1 = 90
Color fila: 5 columna 2 = 101
Color fila: 5 columna 3 = 113
Color fila: 5 columna 4 = 117
Color fila: 5 columna 5 = 119
Color fila: 5 columna 6 = 124
Color fila: 5 columna 7 = 132
Color fila: 5 columna 8 = 137
Color fila: 6 columna 0 = 97
Color fila: 6 columna 1 = 119
Color fila: 6 columna 2 = 128
Color fila: 6 columna 3 = 138
Color fila: 6 columna 4 = 142
Color fila: 6 columna 5 = 143
Color fila: 6 columna 6 = 147
Color fila: 6 columna 7 = 150
Color fila: 6 columna 8 = 150
Color fila: 7 columna 0 = 127
Color fila: 7 columna 1 = 143
Color fila: 7 columna 2 = 151
Color fila: 7 columna 3 = 158
Color fila: 7 columna 4 = 160
Color fila: 7 columna 5 = 160
Color fila: 7 columna 6 = 161
Color fila: 7 columna 7 = 160
Color fila: 7 columna 8 = 157
Color fila: 8 columna 0 = 147
Color fila: 8 columna 1 = 162
Color fila: 8 columna 2 = 166
Color fila: 8 columna 3 = 168
Color fila: 8 columna 4 = 166
Color fila: 8 columna 5 = 165
Color fila: 8 columna 6 = 165
Color fila: 8 columna 7 = 163
Color fila: 8 columna 8 = 158

```
</details>
{::options parse_block_html="false" /}

***


> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

1. OpenCV. *Accessing and Modifying pixel values*
 [https://docs.opencv.org/3.4/d3/df2/tutorial_py_basic_ops.html](https://docs.opencv.org/3.4/d3/df2/tutorial_py_basic_ops.html)


