---
title: Listar archivos de una carpeta en python
date: 2021-11-03 00:01:00 +0300
categories: [Python, Python básico]
tags: [python, openCV, directorio, os, listdir, path, windows, ubuntu]
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1192/v1636478056/kipunaEC/listarArchivos/portadaBlogLista-min_qn9tpi.png
redirect_to: https://kipunaec.com/listar-archivos-de-una-carpeta-en-python/
---

***

Escribo este post porque en tutoriales anteriores como: [crear un video con frames](../Crear-un-video-con-frames-openCV-python/) o [crear un gif con imagenes](../Crear-un-gif-con-imagenes-imageio-python/) que se desarrollaron inicialmente en `Ubuntu`, y luego al intentar migrar esos códigos a `windows` aparecían errores porque el `path` que contiene los archivos no estaba corrrectamente asignado. 

*Nota:* Para que un programa lea correctamente los directorios, la clave esta en colocar bien el **slash** <b style='color:green'> / </b> y **back slash**<b style='color:green'> \ </b> ¡Empecemos!

# Listar archivos de una carpeta en python
Crearé un ejemplo con el [módulo os](https://docs.python.org/3/library/os.html) en el que listaré los archivos de una misma carpeta en **Windows** y **Ubuntu** para comparar cómo los directorios se escriben de diferente manera en estos sistemas operativos.

## Módulo os
Permite acceder a funcionalidades del Sistema Operativo y manipular la estructura de directorios. Esté módulo tiene varias funciones como:  `os.ctermid()`, `os.getcwd()`, `os.chmod` y muchas más que se pueden revisar por completo en el [link oficial módulo os](https://docs.python.org/3/library/os.html). La función que detallaré en este post es [os.listdir](https://docs.python.org/3/library/os.html#os.listdir) que permite listar los archivos de una carpeta.  

### os.listdir()
Esta función devuelve una lista con los nombres de los archivos que se encuentran en un directorio. 

A continuación en **Gif 1** y **Gif 2** se muestran `5` archivos de la `carpeta01` en ubuntu y windows respectivamente. Adicionalmente se muestran como obtener en `path` de la carpeta en cada sistema operativo.

![archivos_Ubuntu](https://res.cloudinary.com/dxh1bpaim/image/upload/v1636196171/kipunaEC/listarArchivos/dirUbuntu_dcp8ps.gif)
_Gif 1. Archivos de la carpeta01 en UBUNTU, y obtener el path_

![archivos_windows](https://res.cloudinary.com/dxh1bpaim/image/upload/v1636477046/kipunaEC/listarArchivos/dirWindows_jad5rn.gif)
_Gif 2. Archivos de la carpeta01 en WINDOWS, y obtener el path_

*Nota: La forma de escribir los directorios en UBUNTU y WINDOWS es diferente*

De acuerdo como se muestra en **Gif 1**, para **ubuntu** el path se debe poner de la siguiente manera para listar los elementos `/home/kipuna/Escritorio/carpeta01`

```python
import os

archivos = os.listdir('/home/kipuna/Escritorio/carpeta01')
print(archivos)
```

```terminal
['ImagenesGif', 'IMG_20210217.jpg', 'Classification_SVM.PDF', 'BITACORA.docx', 'pedestrianDetection.pdf']
```
Y de acuerdo a **Gif 2** para **windows**, el path aparece asi: `C:\Users\kipuna\Desktop\carpeta01` pero se debe modificar con *slash simples* así `C:/Users/kipuna/Desktop/carpeta01`

```python
import os

archivos = os.listdir('C:Users/Desktop/carpeta01')
print(archivos)
```

```terminal
['ImagenesGif', 'IMG_20210217.jpg', 'Classification_SVM.PDF', 'BITACORA.docx', 'pedestrianDetection.pdf']
```

***

[Gif]: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_728/v1633444807/kipunaEC/gifs/patricio5_h2janv.gif
[suscribirse]: https://www.youtube.com/channel/UCLHyReaGzfUcaiGoEN5jXEA "Clic para suscribirse en youtube"
[![Suscribirse][Gif]][suscribirse]

***


***
## video

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/fiilnEu1_vM" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

*** 

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: OpenCV documentación. *Canny Edge Detection*. [https://docs.opencv.org/3.4/da/d22/tutorial_py_canny.html](https://docs.opencv.org/3.4/da/d22/tutorial_py_canny.html)
