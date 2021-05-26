---
title: Extraer frames de un video con openCV y python
date: 2021-05-16 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, frames, video, guardar]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1621263423/kipunaEC/extraerFrames/portada1_shwvpr.gif
---

***

## Extraer frames de un video

Este post registra como obtener varios frames de un video. 
El **video 1** `gato.mp4` que se muestra a continuación tiene una duración de 6 segundos y 30 frames por segundo, ver en **Fig 1** y con este obtengo aproximadamente 180 frames nombrados desde `IMG_0001.jpg`, `IMG_0002.jpg`, `IMG_0003.jpg`...

<center>
<video src="https://res.cloudinary.com/dxh1bpaim/video/upload/c_scale,w_250/v1621257471/kipunaEC/extraerFrames/gato_ujxhni.mp4" controls>
  Tu navegador no implementa el elemento <code>video</code>.
</video>
</center>
<center>
<p style="color: rgb(133,149,138);"> Video 1. gato.mp4 </p>
</center>

![propiedades de video 1](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_360/v1621257677/kipunaEC/extraerFrames/propiedades_nztvq0.png)
_Fig 1. Propiedades de Video 1_

El programa a continuación extrae los frames de **Video 1**

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>

1. `import cv2` importar openCV
2. `capture = cv2.VideoCapture('gato.avi')` leer el archivo `gato.avi`
3. `cont = 0` contador iniciado en `0` se usará para nombrar consecutivamente los frames
4. `path = '/home/noemi/Escritorio/Proy_Ocv/ocv-python-Extraer-frames/frames/'` ubicación donde se almacenarán los frames extraídos
4. `while (capture.isOpened()):`
 * `capture.isOpened()` Devuelve `True` si la captura de video ya se ha inicializado.
5. `ret, frame = capture.read()`, usa el objeto `capture` para leer la información de la webCam
 * `frame` información del video frame por frame
 * `ret` valor booleano `TRUE` si `frame` es leído correctamente 
6. `if (ret == True)`, si `ret` es `True` ejecutará lo que este dentro de la sentencia `if`. 
7. `cv2.imwrite(path + 'IMG_%04d.jpg' % cont, frame)` escribe los frames en la ubicación especificada.
 * `path`dirección donde se guardarán los frames
 * `'IMG_%04d.jpg'` nombre de las imágenes, se guardará como `IMG_0001.jpg`, `IMG_0002.jpg`, `IMG_0003.jpg` ...
 * `cont += 1`la variable contador aumenta un valor en cada iteración
8. `if (cv2.waitKey(1) == ord('s')):`, sentencia  [if](https://docs.python.org/3/tutorial/controlflow.html) compara dos valores, si se presiona la tecla `s` cumple la condición termina el bucle. Revisar también [Cómo funciona (cv2.waitKey(1) & 0xFF) == ord(‘s’)
](../Mostrar-la-webCam-o-reproducir-un-video-openCV-python/#como-funciona-cv2waitkey1--0xff--ords) 
9. `capture.release()` para liberar la captura
10. `cv2.destroyAllWindows()` cerrar todas las ventanas

</details>
{::options parse_block_html="false" /} 
  

```python
import cv2

capture = cv2.VideoCapture('gato.mp4')
cont = 0
path = '/home/noemi/Escritorio/Proy_Ocv/ocv-python-Extraer-frames/frames/'

while (capture.isOpened()):
    ret, frame = capture.read()
    if (ret == True):
        cv2.imwrite(path + 'IMG_%04d.jpg' % cont, frame)    
        cont += 1
        if (cv2.waitKey(1) == ord('s')):
            break
    else:
        break

capture.release()
cv2.destroyAllWindows()
```

![resultado](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1621223239/kipunaEC/extraerFrames/frames_tlvhvn.png)
_Fig 2. Frames extraídos de Video 1_

Obtuve en total 184 frames, porque el video duró un poco mas de 6 segundos. 

<a class="github-button" href="https://github.com/kipunaEc/Python-OpenCV-extraerFrames" data-style="mega">Revisa este código en github</a>
<script async defer src="https://buttons.github.io/buttons.js"></script>

*** 

> Aprendan siempre, aprendan mucho — Mimi

***

