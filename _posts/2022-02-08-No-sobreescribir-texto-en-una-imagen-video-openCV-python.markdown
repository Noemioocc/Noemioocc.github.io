---
title: No sobreescribir texto en una imagen openCV - python
date: 2022-02-08 00:01:00 +0300
categories: [Python, openCV]
tags: [python, openCV, texto, sobreescribir, decimales, format, imagen, video]
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_340/v1644373548/videoTextoa_g6fhfv.gif
---

***
En este post detallo como no sobreescribir el texto en una imagen. Usaré un post anterior [añadir texto a una imagen openCV python](../Añadir-texto-a-una-imagen-openCV-python/) con modificaciones para que el texto no se sobreescriba, tambien muestro como poner texto en un video. 

# Copy() 
Usaremos esta función para obtener un arreglo con las caracteristicas de la imagen original.

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/6620s-6x6pE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>

</div>

# Texto en imágenes sin sobreescribir

Despues de leer la imagen con openCV, puedo usar los siguiente código:
`imagen.copy()`o también usando numpy `np.copy(imagen)`

*¡Veamos cómo va el código completo!*

![numeros](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_420/v1644363351/kipunaEC/noSobreescribirText/numeros_ykmenp.gif)
_Resultado del código - números sobre una imagen_

```python
#Importar biblioteca openCV
import cv2
#Leer imagen y redimensionar
img = cv2.imread('Quito.jpg')
img = cv2.resize(img, (720, 570))
#Características del texto
ubicacion = (20,150)
tipoLetra = cv2.FONT_HERSHEY_TRIPLEX
tamañoLetra = 5
colorLetra = (221,82,196)
grosorLetra = 2
#Escribir numeros del 1 al 20
for i in range(20):
    #Copiar imagen
    img2 = img.copy()
    #Escribir Texto
    cv2.putText(img2, str(i), ubicacion, tipoLetra, tamañoLetra, colorLetra, grosorLetra)
    #Mostrar imagen
    cv2.imshow('Imagen',img2)
    cv2.waitKey(200)

cv2.destroyAllWindows()
```

En el siguiente código pongo números aleatorios y muestro varios decimales, algunas veces se necesita reducir los decimales para hacer eso puedo usar cualquiera de siguientes lineas de código [^1]:

* `"%.2f[unidades]" % (texto)`  el resultado será `0.96[unidades]`
* `"{:.2f}[unidades]".format(0.964545)` el resultado será `0.96[unidades]`
* `f'{0.964545:.2f}[unidades]'` el resultado será `0.96[unidades]`

![numerosaleatorios](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_420/v1644365191/kipunaEC/noSobreescribirText/nosobreescribir2_yhdnkv.gif)
_Resultado del código - números aleatorios en una imagen_

```python
#Importar biblioteca openCV
import cv2
import numpy as np
#Leer imagen y redimensionar
img = cv2.imread('Quito.jpg')
img = cv2.resize(img, (720, 570))
#Características del texto
ubicacion = (20,150)
ubicacion2 = (20,300)
tipoLetra = cv2.FONT_HERSHEY_TRIPLEX
tamañoLetra = 1.9
colorLetra = (255,0,0)
grosorLetra = 2
#Escribir numeros del 1 al 20
for i in range(25):
    texto = np.random.rand()
    #Copiar imagen
    img2 = img.copy()
    #Escribir Texto
    cv2.putText(img2, str(texto), ubicacion, tipoLetra, tamañoLetra, colorLetra, grosorLetra)
    cv2.putText(img2, "%.2f[unidades]" % (texto), ubicacion2, tipoLetra, tamañoLetra, colorLetra, grosorLetra)
    #Mostrar imagen
    cv2.imshow('Imagen',img2)
    cv2.waitKey(200)

cv2.destroyAllWindows()
```
<a class="github-button" href="https://github.com/kipunaEc/Python-OpenCV-noSobreescribirTexto.git" data-style="mega">Revisa este código en github</a>
<script async defer src="https://buttons.github.io/buttons.js"></script>

# Texto en un Video 
A diferencia de las imágenes, cuando se coloca texto en un video no es necesaro usar la función `copy()` porque un video esta compuesto por frames que se actualizan uno tras otro. 

![webCAMaleatorios](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_440/v1644372287/kipunaEC/noSobreescribirText/videoTexto_j6fjvz.gif)
_Web CAM- números aleatorios_


En el siguinte código te muestro donde se suguiere poner el código:
```python
#importar librerías
import cv2
import numpy as np
#Objeto de video cature
capture = cv2.VideoCapture(0)
#Características del texto
texto = "Valores aleatrios"
ubicacion = (10,100)
ubicacion2 = (10,200)
tipoLetra = cv2.FONT_HERSHEY_TRIPLEX
tamañoLetra = 2
colorLetra = (0,255,0)
grosorLetra = 2

while (capture.isOpened()):
    #Leer cada frame
    ret, frame = capture.read()
    if (ret == True):
        #Texto números aleatorios
        numeros = np.random.rand()
        #Colocar texto
        cv2.putText(frame, texto, ubicacion, tipoLetra, tamañoLetra, colorLetra, grosorLetra)
        cv2.putText(frame, "%.5f" % (numeros), ubicacion2, tipoLetra, tamañoLetra, colorLetra, grosorLetra)
        #Mostrar frames
        cv2.imshow("Video", frame)
        #Al presionar la tecla s sale del bucle
        if (cv2.waitKey(1) == ord('s')):
            break
    else:
        break

capture.release()
cv2.destroyAllWindows()
```

<a class="github-button" href="https://github.com/kipunaEc/Python-openCV-TextoVideo.git" data-style="mega">Revisa este código en github</a>
<script async defer src="https://buttons.github.io/buttons.js"></script>

[Gif]: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_728/v1633444807/kipunaEC/gifs/patricio5_h2janv.gif
[suscribirse]: https://www.youtube.com/channel/UCLHyReaGzfUcaiGoEN5jXEA "Clic para suscribirse en youtube"
[![Suscribirse][Gif]][suscribirse]

***

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: WhoisMatt. StackOverflow. *How to change 39.54484700000000 to 39.54 and using python* [https://stackoverflow.com/a/5202318/14827271](https://stackoverflow.com/a/5202318/14827271)
