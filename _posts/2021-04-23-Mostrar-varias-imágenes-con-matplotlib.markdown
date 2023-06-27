---
title: Mostrar imagenes en matplotlib openCV - python
date: 2021-04-23 00:01:00 +0300
categories: [Python, Matplotlib ]
tags: [python, openCV, imagenes, matplotlib]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1619235488/kipunaEC/python-matplotlib-openCV-abrir-imagenes/imagenMatplotlib_dlmr9b.gif
redirect_to: https://kipunaec.com/mostrar-imagenes-con-matplotlib-opencv-y-python/
---

***

## Matplotlib

 Es una biblioteca completa para crear visualizaciones estáticas, animadas e interactivas en Python. 

![texto-varios-gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_300/v1619209037/kipunaEC/python-matplotlib-openCV-abrir-imagenes/matplotlib-logo_wwxhbu.png)
_Fig 1. Logo matplotlib_

[Matplotlib](https://matplotlib.org/stable/index.html) puede mostrar varios tipos de gráficas como funciones aritméticas, graficos de barras, gráficas estadísticas etc. En este post registro como mostrar una imagen con matplotlib, esta imagen será previamente cargada con [imread](https://docs.opencv.org/3.4/d4/da8/group__imgcodecs.html#ga288b8b3da0892bd651fce07b3bbd3a56) de openCV

***

[banner]:  https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_728/v1624132126/kipunaEC/banner/CursoBigData_s1a7oz.gif
[bigData]: https://go.hotmart.com/F54793255L "Comprar curso de Python para data science y big data"
[![logo de yanbal][banner]][bigData]

***

## Mostrar una imagen con matplotlib

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código  **Clic para desplegar** 
</summary>

1. `import cv2`, cargar [openCV](https://opencv.org/) 
2. `import matplotlib.pyplot as plt`, en la librería [matplotlib](https://matplotlib.org/stable/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py) le asigno un alias `plt`
3. `imgBGR = cv2.imread('Tren.png')` 
 * Leo la imagen **Tren.jpg** con la función [imread](https://docs.opencv.org/3.4/d4/da8/group__imgcodecs.html#ga288b8b3da0892bd651fce07b3bbd3a56) de openCV.
 * *Nota: OpenCV carga las imágenes en formato **B G R**, y matplotlib muestra las imagenes en formato **R G B** por eso se debe cambiar el espaco de color de la imagen antes de mostrarla, caso contrario mostrará colores distintos*
4. `imgRGB = cv2.cvtColor(imgBGR, cv2.COLOR_BGR2RGB)` 
 * [Cambio el espacio de color](../Cambio-de-espacio-de-color-openCV-python/) desde **B G R**  a  **R G B**, usando la función [cvtColor](https://docs.opencv.org/3.4/d8/d01/group__imgproc__color__conversions.html#ga4e0972be5de079fed4e3a10e24ef5ef0)
5. `plt.xticks([]), plt.yticks([])` evita que aparezcan ejes en la figura
6. `plt.imshow(imgRGB')`, identifica que imagen mostrar
7. `plt.show()` ,muestra la imagen  

</details>
{::options parse_block_html="false" /} 

```python
#importar librerias openCV, matplotlib
import cv2
import matplotlib.pyplot as plt
#Cargar la imagen con openCV
imgBGR = cv2.imread('Tren.png')
#Cambiar esacio de color BGR a RGB
imgRGB = cv2.cvtColor(imgBGR, cv2.COLOR_BGR2RGB)
#Mostrar imagen
plt.xticks([]), plt.yticks([])
plt.imshow(imgRGB, cmap='gray', interpolation='bicubic')
plt.show()
```

![texto-varios-gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_400/v1619210781/kipunaEC/python-matplotlib-openCV-abrir-imagenes/trenFig1-_e7yv1l.png)
_Fig 2. Imagen mostrada con matplotlib_

## Mostrar varias imágenes en una sola figura

Con matplotlib puedo mostrar varias imágenes en una misma figura, las imagenes que usaré estan en una carpeta donde solo se encuentran las imagenes  `Amazonía.jpg, Cotopaxi.jpg, Galápagos.jpg, Manta.jpg, Otavalo.png, Quilotoa.jpg, Quito.jpg, Salinas.jpg, Tren.png` 

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>

1. `import cv2` importar librerías opeCV
2. `import matplotlib.pyplot as plt` importar matplotlib con un alias `plt`
3. `import os` importar módulo OS para acceder a las imagenes desde un direcrio específico
4. Identificar la ruta de las imágenes
 * `dirCarpeta = '/home/noemi/Escritorio/Proy_Ocv/Matplotlib/Matplotlib-mostrar-imagen/ImagenesEcuador/'`
 * `archivos = os.listdir(path)`, método [listdir](https://docs.python.org/es/3.10/library/os.html#os.listdir) crea una lista con los archivos que existen en `dirCarpeta` 
5. Definir arreglos vacíos para luego llenarlos con datos
 * `img_array = []` para datos de imagenes
 * `titulos_array = []` para títulos
6. Bucle [for](https://docs.python.org/3/tutorial/controlflow.html#for-statements)
 * `dirArchivo = dirCarpeta + archivos[x]` direccion y nombre de la imagen en una misma variable
 * `imgBGR = cv2.imread(dirArchivo)` leer la imagen con openCV
 * `imgRGB = cv2.cvtColor(imgBGR, cv2.COLOR_BGR2RGB)` cambiar el espacio de color **B G R** a **R G B**
 * `img_array.append(imgRGB)` llenar el arreglo `img_array` con las imágenes que se leyero el la lìnea anterior
 * `img_ext = archivos[x]` guardar el nombre de la imagen y la extensión en la variable `img_ext`
 * `nomImagen = img_ext[:-4]` eliminar la extensión `.jpg` o `.png` del nombre de la imagen
 * `titulos_array.append(nomImagen)` crear un arreglo con todos los nombres de las imagenes
 * `plt.subplot(3, 3, x + 1)` especifica la cantidad de filas y columnas que tendrá la figura. `x+1` ubica a las imagenes en una posición específica
 * `plt.xticks([]), plt.yticks([])` ocultar valores numéricos de los ejes
 * `plt.xlabel(titulos_array[x])` escribe los nombres de cada imagen debajo de las mismas
 * `plt.imshow(img_array[x])` identifica que imagen mostrará
 * `plt.savefig('LugaresEcuador.jpg')` guardar la imagen
 * `plt.show()` Mostrar imagen

</details>
{::options parse_block_html="false" /} 
    
```python
#importar librerias openCV, matplotlib
import cv2
import matplotlib.pyplot as plt
import os
#Identificacion de los archivos de imagen
dirCarpeta = '/home/noemi/Escritorio/Proy_Ocv/Matplotlib/Matplotlib-mostrar-imagen/ImagenesEcuador/'
archivos = os.listdir(dirCarpeta)
#Arreglos vacios
img_array = []
titulos_array = []

for x in range(0, len(archivos)):
    dirArchivo = dirCarpeta + archivos[x]
    #Cargar la imagen con openCV
    imgBGR = cv2.imread(dirArchivo)
    #Cambiar esacio de color BGR a RGB
    imgRGB = cv2.cvtColor(imgBGR, cv2.COLOR_BGR2RGB)
    #Arreglo con la informacion de las imagenes leidas
    img_array.append(imgRGB)
    #Extraer el nombre de la imagen sin la extension
    img_ext = archivos[x]
    nomImagen = img_ext[:-4]
    #Nombres de imagenes ser[an un arreglo de titulos
    titulos_array.append(nomImagen)
    #Establecer filas y comulnas de la figura
    plt.subplot(3, 3, x + 1)
    #Ocultar valores numericos de los ejes
    plt.xticks([])
    plt.yticks([])
    #Colocarl los titulos en cada imagen
    plt.xlabel(titulos_array[x])
    #Identifica que imagen mostrar
    plt.imshow(img_array[x])
#Titulo de la figura
plt.suptitle('Lugares del Ecuador')
#Guardar la imagen
plt.savefig('LugaresEcuador.jpg')
#Mostrar imagen
plt.show()

```
![varias-imagenes](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1619232955/kipunaEC/python-matplotlib-openCV-abrir-imagenes/variasImagenes_xpe7qu.png)
_Fig 3. Varias imagenes en la misma figura_

<a class="github-button" href="https://github.com/kipunaEc/Python-OpenCV-Mostrar-Imagenes-Matplotlib" data-style="mega">Revisa este código en github</a>
<script async defer src="https://buttons.github.io/buttons.js"></script>

***
<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/OUF531ctFQY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

***

> Aprendan siempre, aprendan mucho  — Mimi

***

## Referencias
1. Jeru Luke. (1 de Julio del 2018). *How to fill a polyline in OpenCV* Disponible en: [https://stackoverflow.com/questions/51121978/how-to-fill-a-polyline-in-opencv](https://stackoverflow.com/questions/51121978/how-to-fill-a-polyline-in-opencv)
2. OpenCV. *Drawing Functions*
 [https://docs.opencv.org/3.4/d6/d6e/group__imgproc__draw.html#ga57be400d8eff22fb946ae90c8e7441f9](https://docs.opencv.org/3.4/d6/d6e/group__imgproc__draw.html#ga57be400d8eff22fb946ae90c8e7441f9)
