---
title: Crear un GIF con imágenes - imageio python
date: 2020-12-22 00:01:00 +0300
categories: [Python, imageio ]
tags: [gif, python, imageio ]
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_400/v1610815205/kipunaEC/frames-to-gif/gato_pn82fv.gif
---
***

## Gif

Es un formato de imagen sin sonido y de poca duración que se repite ciclicamente, es más pesado que formatos `jpg` y `png`. Para crear un gif a partir de varias imágenes en este post se usa la libería [imageio](https://pypi.org/project/imageio/).

***

## Imageio

[imageio](https://pypi.org/project/imageio/) es una librería para python que proporciona una interfaz para leer y escribir imágenes. 

***

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/Div2G8Su6r4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

***

## Crear Gifs con varias imágenes

![pixel-imagen](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612390887/kipunaEC/frames-to-gif/imggif_drzeo7.jpg)
_Fig 1. imágenes para crear gif_

El siguiente código muestra como crear un gif con 6 imágenes **Fig 1** *(Mis imágenes pesan máximo 111kb)*. 
1. Importar librerías [imageio](https://pypi.org/project/imageio/), [os](https://docs.python.org/3/library/os.html)
2. Crear variables
 * `path`, directorio de las imágenes 
 * `archivos`, lista de archivos en *path* 
 * `img_array = []`, arreglo vacío 
3. Leer imágenes en un bucle [for](https://docs.python.org/3/tutorial/controlflow.html#for-statements)
 * `len(archivos)` Procurar que no sea una cantidad de imágenes muy grande porque **los archivos GIF son pesados**
 * `nomArchivo = archivos[x]` guarda el nombre del archivo según la iteración del bucle for
 * `dirArchivo` guarda la dirección `+` el nombre del cada archivo
 * [imageio.imread](https://imageio.readthedocs.io/en/stable/userapi.html) lee la imagen desde un directorio, **las imágenes deben ser del mismo tamaño** 
 * `img_array.append` Agregar imágenes el arreglo 
 * Guardar la imagen en formato `gif` con [imageio.mimwrite](https://imageio.readthedocs.io/en/stable/userapi.html)
   * `'auto.gif'` nombre del archivo *gif* se escribe entre comillas   
   * `img_array` arreglo de imágenes que se van a guardar en formato *gif* 
   * `'GIF'` formato de salida 
   * `duration = 0.5` duración de cada fotograma en segundos  
 

```python
# Importra librerías
import os
import imageio

# Ubicación de la base de datos
path = '/home/noemi/Escritorio/Proy_Ocv/imageio-python-crearGif/ImagenesGif/'
archivos = sorted(os.listdir(path))
img_array = []

#Leer todos los archivos formato imagen desde path
for x in range(0, len(archivos)):
    nomArchivo = archivos[x]
    dirArchivo = path + str(nomArchivo)
    
    #Asignar a variable leer_imagen, el nombre de cada imagen
    leer_imagen = imageio.imread(dirArchivo)
    
    # añadir imágenes al arreglo img_array
    img_array.append(leer_imagen)
    
#Guardar Gif
imageio.mimwrite('Gato.gif', img_array, 'GIF', duration=0.5)
```

***


> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

1. Pomain Buthi. (20 de Junio del 2020), *How To Build GIF/Video From Images With Python Pillow/Opencv* . Publicado en: [https://pomain.medium.com/how-to-build-gif-video-from-images-with-python-pillow-opencv-c3126ce89ca8](https://pomain.medium.com/how-to-build-gif-video-from-images-with-python-pillow-opencv-c3126ce89ca8)
