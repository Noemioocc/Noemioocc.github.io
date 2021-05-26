---
title: Mostrar la webCam o reproducir un video con openCV y python
date: 2021-05-11 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, webcam, video, reproducir, mostrar]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1621181124/kipunaEC/webCam/portada_qy7jvz.gif
---

***

## Mostrar la webCam openCV python

El siguiente programa describe como mostrar el contenido de la webCam, también aplica para cámaras externas, pero se debe modificar el valor en `cv2.VideoCapture()` de acuerdo al puerto donde se conecte la cámara. En **Video 1** se muestra el resultado del código.

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>

1. `import cv2`, importar la librería de openCV 
2. `capture = cv2.VideoCapture(0)`, crear un objeto `capture` de `VideoCapture(0)`
 * Tiene como argumento `0` para leer la webCam. También recibe valores como -1, 1, etc si se conecta en otros puertos otras cámaras.
3. `while (capture.isOpened()):`
 * `capture.isOpened()` Devuelve `True` si la captura de video ya se ha inicializado.
4. `ret, frame = capture.read()`, usa el objeto `capture` para leer la información de la webCam
 * `frame` información del video frame por frame
 * `ret` valor booleano `TRUE` si `frame` es leído correctamente 
5. `if (cv2.waitKey(1) == ord('s')):`, sentencia  [if](https://docs.python.org/3/tutorial/controlflow.html) compara dos valores, si se cumple la condición termina el bucle.
 * `cv2.waitKey(1)`, si una tecla es presionada, regresa un valor de acuerdo al código [ascii](http://www.asciitable.com/), mientras no se presione una tecla devuelve el valor de `-1` 
 * `ord('s')` la función [ord](https://docs.python.org/3/library/functions.html#ord) recibe un caracter y devuelve un valor que representa a ese caracter.
 * La condición [^1]  queda de la siguiente manera: `(cv2.waitKey(1) == ord('s'))` --> `1110011 == 01110011` (Cuando se cuple, sale del bucle)
6. `capture.release()` para liberar la captura
7. `cv2.destroyAllWindows()` cerrar todas las ventanas

</details>
{::options parse_block_html="false" /} 
  

```python
import cv2

capture = cv2.VideoCapture(0)

while (capture.isOpened()):
    ret, frame = capture.read()
    cv2.imshow('webCam',frame)
    if (cv2.waitKey(1) == ord('s')):
        break

capture.release()
cv2.destroyAllWindows()
```

![webCam](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_400/v1621899376/kipunaEC/webCam/miniatura00_kdoten.png)
_Fig 1. WebCam_

*Nota:* En este ejemplo uso `(cv2.waitKey(1) == ord('s'))` para salir del bucle, en la documentación oficial de openCV [^2]  usa `((cv2.waitKey(1) & 0xFF) == ord('s'))` en la siguiente sección explico el funcionamiento de esta sentencia.



***

## Como funciona (cv2.waitKey(1) & 0xFF) == ord('s')

La documentación de openCV [Getting Started with Videos](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_gui/py_video_display/py_video_display.html) para salir del bulce usa el siguiente comando, que realiza una comparación entre dos valores igual que el ejemplo anterior pero añade `0xFF`.  
```python
if ((cv2.waitKey(1) & 0xFF) == ord('s'))`
```

1. Primero `(cv2.waitKey(1) & 0xFF)` con `&` realiza una operación AND de bits a bits *(Nota: No confundir con `AND` que realiza operaciones `booleanas`)* 
 * Dependiendo de la tecla que se presione `cv2.waitKey(1)` devolverá un entero (Para el ejemplo se presiona la tecla `s` que representa en ascii `115` y en binario `1110011`). 
 * Y `0xFF` representa en binario `11111111`
2. La operación AND de bit a bit queda de la siguiente manera si se presiona la letra `s`
 * `((cv2.waitKey(1) & 0xFF) == ord('s'))`
 * `((01110011 & 11111111) == 01110011)`
 * `1110011 == 01110011`
 * La condición se cumple y sale del bucle

***

## Guardar un video con la webCam openCV python

Para guardar el video se debe agregar el objeto `salida` de [VideoWriter](../VideoWriter-openCV-python/) y así establecer las características del video

```python
salida = cv2.VideoWriter('webCam.avi', cv2.VideoWriter_fourcc(*'XVID'), 10, (640,480))
```
También  se usa el método `.write` para poner cada frame en el video 'webCam.avi'
```python
salida.write(frame)
```
A continuación se describe el código que guarda un video desde la webCam

```python
import cv2

capture = cv2.VideoCapture(0)
#objeto salida, contiene los parámetros para crear el video
salida = cv2.VideoWriter('webCam.avi', cv2.VideoWriter_fourcc(*'XVID'), 10, (640,480))

while (True):
    ret, frame = capture.read()
    cv2.imshow('frame',frame)
    #Usar write para GUARDAR el video
    salida.write(frame)
    if (cv2.waitKey(1) == ord('s')):
        break

capture.release()
cv2.destroyAllWindows()
```
***

# Reproducir un video openCV python 

El programa para reproducir un video desde un directorio es similar al anterior, varía que, en lugar de colocar un valor como `0` en `VideoCapture`, se debe asignar el nombre del video `'gato.avi'` (si se encuentra en la misma carpeta que el programa) o colocar la dirección en donde este video se encuentre, y también le añado un bucle `if (ret == True)` porque en algún frame el video se terminará y sin esta condición saldra un error porque no encontrará frame que mostrar. 

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>

1. `import cv2`, importar la librería de openCV 
2. `capture = cv2.VideoCapture('gato.avi')`, crear un objeto `capture` de `VideoCapture(0)`
 * Tiene como argumento entre comillas el nombre del video. También se puede usar el path del video `cv2.VideoCapture('/home/noemi/Escritorio/reproducir_Videos/gato.avi')`
3. `while (capture.isOpened()):`
 * `capture.isOpened()` Devuelve `True` si la captura de video ya se ha inicializado.
4. `ret, frame = capture.read()`, usa el objeto `capture` para leer la información de la webCam
 * `frame` información del video frame por frame
 * `ret` valor booleano `TRUE` si el `frame` es leído correctamente 
5. `if (ret == True)`, si `ret` es `True` ejecutará lo que este dentro de la sentencia `if`. 
6. `if (cv2.waitKey(30) == ord('s')):`, sentencia  [if](https://docs.python.org/3/tutorial/controlflow.html) compara dos valores, si se cumple la condición termina el bucle.
 * `cv2.waitKey(30)`, si una tecla es presionada, regresa un valor de acuerdo al código [ascii](http://www.asciitable.com/), mientras no se presione una tecla devuelve `-1`. *Nota: algunos videos pueden reproducirse mas rápido o mas lento de acuerdo a las características como el bitrate, openCV tratará de reproducir el archivo rápido, para modificar eso se puede variar el valor* de `cv2.waitKey(30)`
 * `ord('s')` la función [ord](https://docs.python.org/3/library/functions.html#ord) recibe un caracter y devuelve un valor que representa a ese caracter.
 * La condición [^1]  queda de la siguiente manera cuando se presiona la tecla `s`: `(cv2.waitKey(1) == ord('s'))` --> `01110011 == 01110011`
6. `capture.release()` para liberar la captura
7. `cv2.destroyAllWindows()` cerrar todas las ventanas

</details>
{::options parse_block_html="false" /} 

```python
import cv2

capture = cv2.VideoCapture('gato.avi')

while (capture.isOpened()):
    ret, frame = capture.read()
    if (ret == True):
        cv2.imshow("gato0", frame)
        if (cv2.waitKey(30) == ord('s')):
            break
    else:
        break

capture.release()
cv2.destroyAllWindows()
```

***

https://es.stackoverflow.com/questions/295916/c%C3%B3mo-guardar-correctamente-un-v%C3%ADdeo-con-opencv

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: Daniel Copley. (09 de octubre del 2016). *¿Para qué es 0xFF en cv2.waitKey (1)?*. Disponible en [https://www.it-swarm-es.com/es/python/para-que-es-0xff-en-cv2.waitkey-1/824142736/](https://www.it-swarm-es.com/es/python/para-que-es-0xff-en-cv2.waitkey-1/824142736/)

[^2]: OpenCV. *Getting Started with Videos* [https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_gui/py_video_display/py_video_display.html](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_gui/py_video_display/py_video_display.html)
