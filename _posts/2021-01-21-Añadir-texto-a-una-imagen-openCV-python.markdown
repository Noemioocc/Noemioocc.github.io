---
title: Añadir texto a una imagen openCV python
date: 2021-01-21 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, texto, imagen, putText, formas]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612374454/kipunaEC/imagen-texto/texto_f9thx8.gif
redirect_to: https://kipunaec.com/anadir-texto-a-una-imagen-opencv-python/
---

***

## Texto en una imagen **putText**

[putext](https://docs.opencv.org/master/d6/d6e/group__imgproc__draw.html#ga5126f47f883d730f633d74f07456c576) es una función de openCV que agrega texto en una posición, tipo, tamaño, color y grosor específicos. 

```python
cv2.putText(img, texto, ubicacion, font, tamañoLetra, colorLetra, grosorLetra, bottomLeftOrigin = False)
```
Antes de escribir sobre una imagen hay que considerar las dimensiones de la misma, para que la posición del texto no este fuera de los límites. A continuación se describe el código:

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>

1. [cv2](https://opencv.org/) librería openCV
2. `img` imagen donde se va a escribir el texto
2. `texto` cadena de caracteres que aparecerá en la imagen
3. `ubicacion` tiene dos coordenadas `ancho, alto`
 * La posición `(0 , 0)`es la superior izquierda
 * La posición `(2592, 1936)` es la esquina inferior derecha
4. `font` tipo de letra disponible ver [**Tab1.**](#tab1-tipos-de-letra)
5. `tamañoLetra` entero que especifica que tan grande o pequeño se mostrará el texto
6. `colorLetra` se escribe en formato `BGR`
7. `grosorLetra` se muestra el texto más voluminoso
8. `bottomLeftOrigin` es opcional, 
 * `bottomLeftOrigin = False`
 * Por defecto es `False`y la posición `(0,0)` es la superior izquierda
9. `cv2.putText` Escribe texto con todas las características en `img` 


</details>
{::options parse_block_html="false" /} 

```python
#Importar librería cv2
import cv2

#Leer imagen
img = cv2.imread('Quito.jpg')

#Características del texto
texto = "Quito"
ubicacion = (200,700)
font = cv2.FONT_HERSHEY_TRIPLEX
tamañoLetra = 25
colorLetra = (221,82,196)
grosorLetra = 10

#Escribir texto
cv2.putText(img, texto, ubicacion, font, tamañoLetra, colorLetra, grosorLetra)

#Guardar imagen
cv2.imwrite('textoQuito.jpg', img)

#Mostrar imagen
cv2.imshow('imagen',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![representación-gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_550/v1611339416/kipunaEC/imagen-texto/Quito1_hqvwrt.jpg)
_Fig 1. Texto en una imagen de dimensión (2592 x 1963)_

Dibujar formas en una imagen se registra en el post [dibujar formas básicas openCV python](../Dibujar-Formas-básicas-openCV-python/)

#### Tab1. Tipos de letra

 | cv2.FONT_HERSHEY_SIMPLEX = 0	|
 | cv2.FONT_HERSHEY_PLAIN = 1		|
 | cv2.FONT_HERSHEY_DUPLEX = 2	|	
 | cv2.FONT_HERSHEY_COMPLEX = 3	|
 | cv2.FONT_HERSHEY_TRIPLEX = 4	|
 | cv2.FONT_HERSHEY_COMPLEX_SMALL = 5	|
 | cv2.FONT_HERSHEY_SCRIPT_SIMPLEX = 6 |	
 | cv2.FONT_HERSHEY_SCRIPT_COMPLEX = 7 |	
 | cv2.FONT_ITALIC = 16		|	

***

[Gif]: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_728/v1633444807/kipunaEC/gifs/patricio5_h2janv.gif
[suscribirse]: https://www.youtube.com/channel/UCLHyReaGzfUcaiGoEN5jXEA "Clic para suscribirse en youtube"
[![Suscribirse][Gif]][suscribirse]

***


## Tipos de letra en una misma imagen

El siguiente código realiza modificaciones para que se muestre en una misma imagen, varios tipos de letra, cambio de color y grosor.

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>

1. [cv2](https://opencv.org/) librería openCV.
2. `img` imagen donde se va a escribir el texto.
3. `font` definir los tipos de letra
4. [for](https://docs.python.org/3/tutorial/controlflow.html#for-statements), las características de la imagen van a depender del valor `i`en el bucle.
 * `tipoLetra` define como una matriz, los tipos de letra
 * `texto`, Quito
 * `tamañoLetra`, permanece constante 
 * `colorLetra`, color inicial `(221, 256, 10)` y en cada iteración cambio en `B` multiplos de 20, en `G` multiplos de 15 y en `R` multiplos de 50 para que se note el cambio de color.
 `grosorLetra`, cada iteración cambia por multiplos de 3
 * `cv2.putText` Escrie el texto definido con las caracteristicas especificas en `img`
 
 
</details>
{::options parse_block_html="false" /} 
 
```python
import cv2

#Leer imagen
img = cv2.imread('Quito.jpg')

#Tipos de letra - Fuentes de texto
font0 = cv2.FONT_HERSHEY_SIMPLEX
font1 = cv2.FONT_HERSHEY_PLAIN
font2 = cv2.FONT_HERSHEY_DUPLEX
font3 = cv2.FONT_HERSHEY_COMPLEX
font4 = cv2.FONT_HERSHEY_TRIPLEX
font5 = cv2.FONT_HERSHEY_COMPLEX_SMALL
font6 = cv2.FONT_HERSHEY_SCRIPT_SIMPLEX
font7 = cv2.FONT_HERSHEY_SCRIPT_COMPLEX
font8 = cv2.FONT_ITALIC

#Bucle for, escribir 9 veces Quito
for i in range(9):
    #Tipo de letra
    tipoLetra = [font0,font1,font2,font3,font4,font5,font6,font7,font8]
    
    #Texto
    texto = "Quito"
    
    #Tamaño de letra
    tamañoLetra = 10
    
    #Color de letra BGR, cambia conforme cambia i
    colorLetra = (221-20*i, 256-15*i, 10+50*i)
    
    #Grosor de letra, camba a igual que i en multiplos de 4
    grosorLetra = 3*i
    
    #La ubicación mantiene en 100 el eje X (ancho)
    # y cambia en multiplos de 200 el eje Y (alto)
    ubicacion = (100,200+205*i)

    #Escribe el texto en la imagen
    cv2.putText(img, texto, ubicacion, tipoLetra[i], tamañoLetra, colorLetra, grosorLetra, cv2.LINE_AA)

#Guardar imagen
cv2.imwrite('Quito0.jpg', img)

#Mostrar imagen
cv2.imshow('Quito',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![texto-varios-gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_550/v1612373070/kipunaEC/imagen-texto/Quito0_ynoutu.jpg)
_Fig 2. Tipos de texto, color, grosor en una misma imagen_

<a class="github-button" href="https://github.com/kipunaEc/python-openCV-EscribirTextoEnImagen" data-style="mega">Revisa este código en github</a>
<script async defer src="https://buttons.github.io/buttons.js"></script>

***

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/vbvuESv_lMw" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

***

> Aprendan siempre, aprendan mucho — Mimi

***

