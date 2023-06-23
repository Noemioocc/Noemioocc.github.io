---
title: Guardar frames cada cierto tiempo python
date: 2022-04-04 00:01:00 +0300
categories: [Python, openCV]
tags: [python, ubuntu, tiempo, datetime, guardar, frames, imwrite]
image: https://res.cloudinary.com/dxh1bpaim/image/upload/v1649632032/kipunaEC/FramesTiempo/framesTiempo_ezvbbu.gif
redirect_to: https://kipunaec.com/guardar-frames-cada-cierto-tiempo-con-python-opencv/
---

***

En este post detallaré como guardar frames de un video cada cierto tiempo, los almacenaré con el formato de fecha y hora en que fueron guardados así: `IMG-2022-04-05-094709.jpg`.  

Para realizar esto combinaremos el código de un post anterior [Extraer frames de un video](../Extraer-frames-de-un-video-openCV-python/) y [Medir el tiempo transcurrido en python](#medir-el-tiempo-de-ejecución-en-pyhton).

¡Empecemos!

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/wZMfpiZhzLg" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>

</div>


# Medir el tiempo de ejecución en pyhton
Para medir el tiempo transcurrido entre instrucciones usaré el módulo [datetime](https://docs.python.org/3/library/datetime.html). El código es el siguiente:

```python
import datetime as dt

tiempoA = dt.datetime.now()

#Cualquier instrucción python-------------------------------------------
print("¿Cuánto tardará en imprimir el resultado de una multiplicación ?")
print("Resultado de la multiplicación:", 50*50)
#------------------------------------------------------------------------
tiempoB = dt.datetime.now()

tiempoTranscurrido = tiempoB - tiempoA
print("tiempo transcurrido:", tiempoTranscurrido)
```
El resultado de la ejecución del código anterior es:
```terminal
¿Cuánto tardará en imprimir el resultado de una multiplicación ?
Resultado de la multiplicación: 2500
tiempo transcurrido: 0:00:00.000073
```
El resultado es que han transcurrido 73 microsegundos
# Guardar frames cada cierto tiempo en pyhton

Para guardar los frames usaré usaré el código de [Extraer frames de un video](../Extraer-frames-de-un-video-openCV-python/) en el que usamos la biblioteca [openCV](https://opencv.org/) para [acceder a la webCam/reproducir un video](../Mostrar-la-webCam-o-reproducir-un-video-openCV-python/), ese código usaba un contador para nombrar los frames guardados, ahora usaremos el módulo [datetime](https://docs.python.org/3/library/datetime.html) para obtener la hora del sistema y nombrar los frames.

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código **Clic para desplegar** 
</summary>

* `import cv2`: importar biblioteca [openCV](https://opencv.org/) 
* `import datetime as dt`: importar módulo [
datetime](https://docs.python.org/3/library/datetime.html) con un alias dt
* `capture = cv2.VideoCapture(0)` captura información desde la webCam, el valor de `0` va según el puerto donde este conectada la cámara (puede ser -1,1,2,0,etc). También puede ser reemplazada por una dirección para leer un video.

* `tiempoA = dt.datetime.now()`: Guarda en la variable tiempoA la hora exacta en ese momento
* `path`: es la dirección donde se guardarán los frames
* `while (capture.isOpened()):`
    * `capture.isOpened()` Devuelve `True` si la captura de video ya se ha inicializado.
    * `ret, frame = capture.read()`, usa el objeto `capture` para leer la información de la webCam
    * `frame` información del video frame por frame
    * `ret` valor booleano `TRUE` si `frame` es leído correctamente 

* `tiempoB = dt.datetime.now()`: guarda en la variable tiempoB la hora exacta en ese momento
* `tiempoTranscurrido = tiempoB - tiempoA`: calcula el tiempo transcurrido entre el puntoB del código y el puntoA
* `if tiempoTranscurrido.seconds >= 3:`: Si en tiempo transcurrido es mayor o igual a 3 segundos ingresa a la sentencia **if**.
    * `cv2.imwrite`: Guarda el frame como un archivo en un formato específico  
    * `dt.datetime.now().strftime('IMG-%Y-%m-%d-%H%M%S')`: Obtiene la hora actual en el momeno que guardaré la imagen y con `.strftime()` le damos el formato como muestra [format codes](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes). En la tabla I muestro los formats que uso en este ejemplo. 
    * `tiempoTranscurrido = 0`: Colocar en cero el tiempo trascurrido para volver a contar 3 segundos.
    * `tiempoA = dt.datetime.now()`: Establecer un nuevo tiempoA para volver a contar
* `if (cv2.waitKey(1) == ord('s')):`, sentencia  [if](https://docs.python.org/3/tutorial/controlflow.html) compara dos valores, si se cumple la condición termina el bucle.
    * `cv2.waitKey(1)`, si una tecla es presionada, regresa un valor de acuerdo al código [ascii](http://www.asciitable.com/), mientras no se presione una tecla devuelve el valor de `-1` 
    * `ord('s')` la función [ord](https://docs.python.org/3/library/functions.html#ord) recibe un caracter y devuelve un valor que representa a ese caracter.
    * `(cv2.waitKey(1) == ord('s'))` --> `1110011 == 01110011` (Cuando se cumple, sale del bucle)
* `capture.release()` para liberar la captura
* `cv2.destroyAllWindows()` cerrar todas las ventanas


|Tabla I |
| `%Y`  | Año | 0001, 0002, …, 2013, 2014, …, 9998, 9999 |
| `%m` |  Mes |01, 02, …, 12 |
| `%d` | Día  | 01, 02, …, 31 |
| `%H`  | Hora (Reloj de 24 horas) | 00, 01, …, 23 |
| `%M`  | Minutos  | 00, 01, …, 59 |
| `%S`  | Segundos | 00, 01, …, 59 |


 </details>
{::options parse_block_html="false" /} 


```python
import cv2
import datetime as dt

capture = cv2.VideoCapture(0)
#Inicializar  tiempo
tiempoA = dt.datetime.now()
path = '/home/kipuna/Escritorio/frames/'

while (capture.isOpened()):
    ret, frame = capture.read()
    if (ret == True):
        #Almacenar el tiempo actual
        tiempoB = dt.datetime.now()
        #Cuanto tiempo ha pasado desde tiempoA?
        tiempoTranscurrido = tiempoB - tiempoA
        cv2.imshow("webCam", frame)
        #Si han pasado 3 segundos ingresa al if
        if tiempoTranscurrido.seconds >= 3:
            cv2.imwrite(path + dt.datetime.now().strftime('IMG-%Y-%m-%d-%H%M%S') +'.jpg' , frame)
            #Se debe encerar el tiempo trascurrido para voler a contar
            tiempoTranscurrido = 0
            #Se debe establecer un nuevo tiempoA
            tiempoA = dt.datetime.now()
        if (cv2.waitKey(1) == ord('s')):
            break
    else:
        break

capture.release()
cv2.destroyAllWindows()
```


[Gif]: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_728/v1633444807/kipunaEC/gifs/patricio5_h2janv.gif
[suscribirse]: https://www.youtube.com/channel/UCLHyReaGzfUcaiGoEN5jXEA "Clic para suscribirse en youtube"
[![Suscribirse][Gif]][suscribirse]

***

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: WhoisMatt. StackOverflow. *How to change 39.54484700000000 to 39.54 and using python* [https://stackoverflow.com/a/5202318/14827271](https://stackoverflow.com/a/5202318/14827271)
