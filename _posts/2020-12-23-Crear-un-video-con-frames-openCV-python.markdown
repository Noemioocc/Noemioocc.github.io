---
title: Crear un video a partir de frames con openCV python
date: 2020-12-23 14:10:00 +0800
categories: [Python, openCV ]
tags: [openCV, python, ubuntu, imread, frames, video ]
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612480910/kipunaEC/frames-to-video/framesVideo_kmafwl.gif
---

***

## Frames y videos
Algunas veces he querido unir varios frames en un video para visualizar bases de datos de imágenes como [**Caltech**](http://www.vision.caltech.edu/Image_Datasets/CaltechPedestrians/), [**Daimler**](http://www.gavrila.net/Datasets/Daimler_Pedestrian_Benchmark_D/daimler_pedestrian_benchmark_d.html) o simplemente para hacer una animación de tipo stop motion, que juntando varios frames puede aparentar un objeto en movimiento. En este post registro como crear un video a partir de [pocos frames](#pocos-frames) y como hacerlo cuando se trabaja con [mas de 50 frames](#más-de-50-frames) incluso si los nombres [no son números consecutivos](#frames-numéricamente-no-consecutivos), usando [**python**](https://www.python.org/) y [**openCV**](https://opencv.org/).

***

## Frames numéricamente consecutivos

### Pocos frames

Unir los frames `IMG_0001.jpg`, `IMG_0002.jpg`, `IMG_0003.jpg`, `IMG_0004.jpg`, `IMG_0005.jpg`, `IMG_0006.jpg` para hacer un video, es una tarea sencilla ya que están ordenados y son pocos, así que se puede escribir los nombres de cada frame en el código. 

![db0](https://res.cloudinary.com/dxh1bpaim/image/upload/v1609712599/kipunaEC/frames-to-video/db0_jpzzv5.jpg)
_Fig 1. Seis frames ordenados_

En los siguientes ítems se describe el código en python - openCV.

1. Importar `cv2`, librería [**openCV**](https://opencv.org/)  
2. Usar método [**.imread**](https://docs.opencv.org/master/d4/da8/group__imgcodecs.html#ga288b8b3da0892bd651fce07b3bbd3a56) para leer frames
 * Si los frames se encuentran en la misma carpeta que `main.py` escribir el nombre `'IMG_00XX.jpg'`, y si se encuentra en otra carpeta colocar el directorio `'/home/noemi/Escritorio/Proy_Ocv/db_0/IMG_00XX.jpg'`.
3. El video debe tener el mismo tamaño que los frames, [img6.shape[:2]](https://docs.opencv.org/master/d3/df2/tutorial_py_basic_ops.html) devuelve el tamaño de la imagen en filas `height` y columnas `width`. 
4. El objeto `video` de tipo [VideoWriter](../VideoWriter-openCV-python/) contiene las características del video.
 * Se creará con el nombre **'db0.wmv'**, codec **cv2.VideoWriter_fourcc(*'mp4v')**, **2** frames por segundo, y con el **ancho, alto** = `(width,height)`
5. Usar método [.write](https://docs.opencv.org/3.1.0/dd/d9e/classcv_1_1VideoWriter.html#a3115b679d612a6a0b5864a0c88ed4b39) para poner cada frame en el video 'db0.wmv'
6. Usar [.realese](https://docs.opencv.org/3.4/d8/dfe/classcv_1_1VideoCapture.html#afb4ab689e553ba2c8f0fec41b9344ae6) para liberar

```python
#Impotar cv2
import cv2

#Leer imagenes
img1 = cv2.imread('IMG_0001.jpg')
img2 = cv2.imread('IMG_0002.jpg')
img3 = cv2.imread('IMG_0003.jpg')
img4 = cv2.imread('IMG_0004.jpg')
img5 = cv2.imread('IMG_0005.jpg')
img6 = cv2.imread('IMG_0006.jpg')

#Tamaño de la última imagen alto y ancho
height, width  = img6.shape[:2]

#Caracteristicas del video
video = cv2.VideoWriter('db0.wmv',cv2.VideoWriter_fourcc(*'mp4v'),2,(width,height))

# Poner cada frame en video
video.write(img1)
video.write(img2)
video.write(img3)
video.write(img4)
video.write(img5)
video.write(img6)

#liberar recursos
video.release()                                   
```

<center>
<video src="https://res.cloudinary.com/dxh1bpaim/video/upload/c_scale,f_auto,q_92,vc_auto,w_250/v1609712425/kipunaEC/frames-to-video/db0_x3rx00.mp4" controls>
  Tu navegador no implementa el elemento <code>video</code>.
</video>
</center>
<center>
<p style="color: rgb(199,207,210);"> Video 1. Seis frames ordenados en un video </p>
</center>

### Más de 50 frames

Siendo más realistas, las bases de datos contiene miles de imágenes y sería una tarea tediosa escribir de uno en uno los nombres de los frames en el código. Ahora tengo una base de datos con **101** imágenes `IMG_0000.jpg ... IMG_0100.jpg`, leeré los frames y crearé el video con un bucle `for` respectivamente.

![db1](https://res.cloudinary.com/dxh1bpaim/image/upload/v1609715295/kipunaEC/frames-to-video/db1_o4ufc2.jpg)
_Fig 2. Una parte de 101 imágenes_

1. Importar la librería [**openCV**](https://opencv.org/)  `cv2`
2. Se crea un array vacío `img_array` para almacenar los frames 
3. Bucle [for](https://docs.python.org/3/tutorial/controlflow.html#for-statements) para cargar frames del directorio
 * `range (0,101)` establece el inicio y fin del bucle **for** (cantidad de frames)
 * Variable `path` contiene el directorio de la base de datos. Usar **%04d** para leer 4 dígitos así: 0000, 0001, 0002...0100 
 * Objeto `ìmg` usa el método [**.imread**](https://docs.opencv.org/master/d4/da8/group__imgcodecs.html#ga288b8b3da0892bd651fce07b3bbd3a56) para cargar frames
 * Método [.append](https://docs.python.org/3/tutorial/datastructures.html) agrega un elemento `ìmg` al array `ìmg_array`
4. El video debe tener el mismo tamaño que los frames, [img.shape[:2]](https://docs.opencv.org/master/d3/df2/tutorial_py_basic_ops.html) devuelve el tamaño de la imagen en filas `height` y columnas `width`. 
5. El objeto `video` de tipo [VideoWriter](../VideoWriter-openCV-python/) contiene las características del video.
 * Se creará con el nombre **'db1.mp4'**, codec **cv2.VideoWriter_fourcc(*'mp4v')**, **5** frames por segundo, y con el **ancho, alto** = `(3120,4160)`
6. Bucle [for](https://docs.python.org/3/tutorial/controlflow.html#for-statements) crea un video con el arreglo de frames
 * `len(img_array)` contiene el número de ítems del arreglo `ìmg_array`
 * Método [.write](https://docs.opencv.org/3.1.0/dd/d9e/classcv_1_1VideoWriter.html#a3115b679d612a6a0b5864a0c88ed4b39) para poner cada frame en el video 'db0.wmv'
7. Usar [.realese](https://docs.opencv.org/3.4/d8/dfe/classcv_1_1VideoCapture.html#afb4ab689e553ba2c8f0fec41b9344ae6) para liberar

```python
#Librería opencv
import cv2

#Arreglo vacío
img_array = []

#For para leer imagenes desde un directorio
for x in range (0,101):
    path = '/home/noemi/Escritorio/Bases de datos/db1/IMG_%04d.jpg' % x
    img = cv2.imread(path)
    img_array.append(img)

#Tamaño de la última imagen alto y ancho
height, width  = img.shape[:2]

video = cv2.VideoWriter('db1.mp4', cv2.VideoWriter_fourcc(*'mp4v'), 5, (width,height))

#For para guardar frames en un video
for i in range(len(img_array)):
    video.write(img_array[i])

video.release()                                                                
```
<center>
<video src="https://res.cloudinary.com/dxh1bpaim/video/upload/c_scale,vc_auto,w_250/v1609708767/kipunaEC/frames-to-video/db2_eu96a9.mp4" controls>
  Tu navegador no implementa el elemento <code>video</code>.
</video>
</center>
<center>
<p style="color: rgb(199,207,210);"> Video 2. 101 frames en un video </p>
</center>

***

## Frames numéricamente no consecutivos
Ahora, siendo mucho más realistas algunas bases de datos de imágenes no son nombradas consecutivamente como [CVC-08: On-board Sequence Pedestrian Dataset](http://adas.cvc.uab.es/elektra/enigma-portfolio/item2/):
 * `2013_09_20_17_24_45_225000_right.tif` 
 * `2013_09_20_17_24_45_556000_right.tif` 
 * `2013_09_20_17_24_45_870000_right.tif` 

Por lo que es útil poder leer todos los archivos directo desde la carpeta en donde están almacenados. Para eso debemos usar el módulo [os](https://docs.python.org/3/library/os.html) que permite gestionar los archivos del sistema operativo. 

![xmas2](https://res.cloudinary.com/dxh1bpaim/image/upload/v1609711985/kipunaEC/frames-to-video/dbcvc-08_awq8fc.jpg)
_Fig 3. Una parte de CVC-08_

1. Importar la librería [**openCV**](https://opencv.org/)  y [módulo  os](https://docs.python.org/3/library/os.html)
2. Variable `path` dirección que alberga los archivos de la base de datos
3. Variable `archivos`
 * `os.listdir(directorio)` contiene los nombres de todos los archivos presentes en `directorio` **todos los archivos del directorio deben ser imágenes**, si hay documentos escritos al momneto de crear el video aparecerá un error.
 * [sorted](https://docs.python.org/3/howto/sorting.html) ordena los archivos
 * `img_array` arrar vacío para almacenar los frames 
4. Bucle [for](https://docs.python.org/3/tutorial/controlflow.html#for-statements) para cargar frames del directorio
 * `len(archivos)` obtiene la cantidad de archivos en la base de datos
 * `nomArchivo = archivos[x]` guarda el nombre del archivo de acuerdo a la iteración que realice el bucle for
 * `dirArchivo` guarda la dirección y el nombre del cada archivo
 * Objeto `ìmg` usa el método [**.imread**](https://docs.opencv.org/master/d4/da8/group__imgcodecs.html#ga288b8b3da0892bd651fce07b3bbd3a56) para cargar frames
 * Método [.append](https://docs.python.org/3/tutorial/datastructures.html) agrega un elemento `ìmg` al array `ìmg_array`
5. El video debe tener el mismo tamaño que los frames, [img.shape[:2]](https://docs.opencv.org/master/d3/df2/tutorial_py_basic_ops.html) devuelve el tamaño de la imagen en filas `height` y columnas `width`. 
6. El objeto `video` de tipo [VideoWriter](../VideoWriter-openCV-python/) contiene las características del video.
 * Se creará con el nombre **'CVC-08.avi'**, codec **cv2.VideoWriter_fourcc(*'DIVX')**, **20** frames por segundo, y con el **ancho, alto** = `(960,480)`
7. Bucle [for](https://docs.python.org/3/tutorial/controlflow.html#for-statements) crea un video con el arreglo de frames
 * `len(img_array)` contiene el número de ítems del arreglo `ìmg_array`
 * Método [.write](https://docs.opencv.org/3.1.0/dd/d9e/classcv_1_1VideoWriter.html#a3115b679d612a6a0b5864a0c88ed4b39) para poner cada frame en el video 'db0.wmv'
8. Usar [.realese](https://docs.opencv.org/3.4/d8/dfe/classcv_1_1VideoCapture.html#afb4ab689e553ba2c8f0fec41b9344ae6) para liberar


```python
#Importra librerías
import os
import cv2
#Ubicación de la base de datos
path = '/home/noemi/Escritorio/Bases de datos/CVC08/Test/FramesPos/'
archivos = sorted(os.listdir(path))
img_array = []

#Leer imagenes
for x in range (0,len(archivos)):
    nomArchivo = archivos[x]
    dirArchivo = path + str(nomArchivo)
    img = cv2.imread(dirArchivo)
    img_array.append(img)
    
#Dimensiones de los frames alto y ancho
height, width  = img.shape[:2]

#Caracteríasticas video
video = cv2.VideoWriter('CVC-08.avi', cv2.VideoWriter_fourcc(*'DIVX'), 10, (width,height))

#Colocar los frames en video
for i in range(0, len(archivos)):
    video.write(img_array[i])
    
#liberar
video.release()                                                           
```
<center>
<video src="https://res.cloudinary.com/dxh1bpaim/video/upload/ac_none,c_scale,f_mp4,q_40,vc_auto,w_400/v1609903328/kipunaEC/frames-to-video/CVC-08_rkavip.mp4" controls>
  Tu navegador no implementa el elemento <code>video</code>.
</video>
</center>
<center>
<p style="color: rgb(199,207,210);"> Video 3. Frames base de datos CVC-8 en un video </p>
</center>

***

> Cualquier retroalimentación de forma respetuosa es bienvenida, porque el conocimiento debe ser libre  — Mimi

***

## Referencias

1. Ayub Khan. (23 de mayo del 2013). [Publicación en un foro online]. *Creating a video using OpenCV 2.4.0 in python*. Mensaje publicado en [https://stackoverflow.com/questions/14440400/creating-a-video-using-opencv-2-4-0-in-python](https://stackoverflow.com/questions/14440400/creating-a-video-using-opencv-2-4-0-in-python)

2. OpenCV. *Saving a Video*
 [https://docs.opencv.org/master/dd/d43/tutorial_py_video_display.html](https://docs.opencv.org/master/dd/d43/tutorial_py_video_display.html)

