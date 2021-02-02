---
title: Crear un GIF con python - imageio 
date: 2020-12-22 00:01:00 +0300
categories: [Python, imageio ]
tags: [gif, python, imageio ]     # TAG names should always be lowercase
---


## Imageio

[imageio](https://pypi.org/project/imageio/) es una librería para python que proporciona una interfaz para leer y escribir imágenes. 

## Gif

Un `gif` es un formato de imagen sin sonido y de poca duración que se repite ciclicamente, es más pesado que formatos `jpg` y `png`. Para crear un gif a partir de varias imágenes uso [imageio](https://pypi.org/project/imageio/).

## Crear Gifs con varias imágenes

![Markers](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_327/v1610815205/kipunaEC/frames-to-gif/gato_pn82fv.gif){:.thumbnail.bordered, width= 10 }

<center>
<p style="color: rgb(69,103,112);"> Fig 1. GIF imágenes 599 x 599, duración de cada frame 0.5 segundos</p>
</center>


El siguiente código muestra como crear un gif con 6 imágenes *(Mis imágenes pesan máximo 111kb)*. 
1. Importar librerías [imageio](https://pypi.org/project/imageio/), [os](https://docs.python.org/3/library/os.html)
2. Crear variables
 * `path`, directorio de las imágenes 
 * `archivos`, lista de archivos en *path* 
 * `img_array = []`, arreglo vacío 
3. Leer imágenes en un bucle **for** 
 * Procurar que `len(archivos)` no tenga una cantidad de imágenes muy grande porque **los archivos GIF son muy pesados**
 * `nomArchivo = archivos[x]` guarda el nombre del archivo según la iteración del bucle for
 * `dirArchivo` guarda la dirección `+` el nombre del cada archivo
 * [imageio.imread](https://imageio.readthedocs.io/en/stable/userapi.html) lee la imagen desde un directorio, **las imágenes deben ser del mismo tamaño** 
4. Agregar imágenes el arreglo `img_array.append`
5. Guardar la imagen en formato `gif` con [imageio.mimwrite](https://imageio.readthedocs.io/en/stable/userapi.html)
 * El nombre del archivo *gif* se escribe entre comillas `'auto.gif'`  
 * Arreglo de imágenes que se van a guardar en formato *gif* `img_array`
 * Formato de salida `'GIF'`
 * Duración de cada fotograma en segundos `duration = 0.5`  
 

```python
# Importra librerías
import os
import imageio

# Ubicación de la base de datos
path = '/home/noemi/Escritorio/Proy_Ocv/imageio-python-crearGif/ImagenesGif/'
archivos = sorted(os.listdir(path))
img_array = []

for x in range(0, len(archivos)):
    nomArchivo = archivos[x]
    dirArchivo = path + str(nomArchivo)

    # Para imageIO
    each_image = imageio.imread(dirArchivo)
    img_array.append(each_image)
    imageio.mimwrite('matplotlib0.gif', img_array, 'GIF', duration=0.5)


```

## Referencias

1. Pomain Buthi. (20 de Junio del 2020), *How To Build GIF/Video From Images With Python Pillow/Opencv* . Publicado en: [https://pomain.medium.com/how-to-build-gif-video-from-images-with-python-pillow-opencv-c3126ce89ca8](https://pomain.medium.com/how-to-build-gif-video-from-images-with-python-pillow-opencv-c3126ce89ca8)
