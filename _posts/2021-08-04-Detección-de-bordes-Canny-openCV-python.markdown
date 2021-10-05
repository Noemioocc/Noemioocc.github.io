---
title: Detección de bordes Canny - openCV python
date: 2021-08-04 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, canny, detección , bordes]
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1628205958/kipunaEC/canny/cannyBlur_cz6xqm.gif
---

***

# Detector de borde Canny

Es un reconocido algoritmo de visión por computador para detección de bordes, lleva su nombre por su desarrollador John F. Canny.

Este Algoritmo se puede usar en [**openCV**](https://opencv.org/) mediante la función [cv.Canny](https://docs.opencv.org/3.4/da/d22/tutorial_py_canny.html), internamente esta función realiza las siguientes etapas:

* `Noise Reduction` Filtra el ruido en la imagen mediante un filtro gaussiano
* `Finding Intensity Gradient of the Image` Encuentra el gradiente. El  gradiente  define  dos  valores: la dirección en  donde  el  cambio  de intensidad es máximo y la magnitud de esa dirección. 

![gradiente](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_150/v1628180897/kipunaEC/canny/intensidadPixeles_ntpz1g.png)
_Fig 1. El gradiente define la dirección del cambio de intensidad_

* `Non-maximum Suppression` Después de obtener la magnitud y la dirección del degradado, se realiza un escaneo completo de la imagen para eliminar los píxeles no deseados que pueden no constituir el borde. Esto elimina los píxeles que no se consideran parte de un borde. Por lo tanto, solo quedarán líneas finas (bordes candidatos).

* `Hysteresis Thresholding` Esta etapa decide cuáles son los bordes que son realmente bordes y cuáles no. Para esto, necesitamos dos valores de umbral, `minVal` y `maxVal`. 

![canny](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_200/v1628181646/kipunaEC/canny/cannyconcetso_ynjzhy.png)
_Fig 2. Límites Max y Min para determinar un borde_

Revisando *Fig 2*, los bordes con un gradiente de intensidad superior a `maxVal` seguramente serán bordes y aquellos por debajo de `minVal` seguramente no serán bordes, por lo que se descartan. 
Aquellos que se encuentran entre estos dos umbrales se clasifican como bordes o no bordes en función de su conectividad. Si están conectados a píxeles de "borde seguro", se consideran parte de los bordes. De lo contrario, también se descartan.

***

[Gif]: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_728/v1633444807/kipunaEC/gifs/patricio5_h2janv.gif
[suscribirse]: https://www.youtube.com/channel/UCLHyReaGzfUcaiGoEN5jXEA "Clic para suscribirse en youtube"
[![Suscribirse][Gif]][suscribirse]

***

# Canny (cv2.Canny) en una imagen - openCv python 

```python
cv2.Canny(image, minVal, maxVal)
```
Los parámetros son los siguientes:
1. `image` es la imagen gris que va a ser analizada
2. `minVal`, `maxVal` son los valores de umbrales para que el algoritmo el la etapa `Hysteresis Thresholding` decida cuales son contornos 

Para probar Canny, debo usar una imagen de un solo canal, en escala de grises, por eso *Fig 3* debe ser leída con la bandera `0` en `imread`, como se muestra en el código a continuación.

![original](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_450/v1628183070/kipunaEC/canny/libro_vrlokp.jpg)
_Fig 3. Imagen sin aplicar Canny_

![Gris](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_450/v1628184313/kipunaEC/canny/imagenGRis_c5p7vd.png)
_Fig 4. Imagen sin aplicar Canny en escala de Gris_


```python
import cv2

img = cv2.imread('libro.jpg',0)
bordesCanny = cv2.Canny(img,100,200)

cv2.imshow('Img', img)
cv2.imshow('Canny - valMin =100 - valMax = 200', bordesCanny)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

En *Fig 5* se ve que `valMin = 100` y `valMax = 200` dan buenos resultados para la detección de bordes.

![canny](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_450/v1628183623/kipunaEC/canny/canny100200_nxf1er.png)
_Fig 5. Canny, valMin = 100, valMax = 200_

Para probar cambié drásticamente los valores de `valMin = 10` y `valMax = 50`, y en *Fig 6* se ve que aparecen mas bordes que no son útiles. Por lo que no es un valor óptimo para los umbrales.

![canny2](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_450/v1628183686/kipunaEC/canny/cany1050_oeujkd.png)
_Fig 6. Canny, valMin = 10, valMax = 50_

# Canny (cv2.Canny) en un video - openCv python 

Uso el código para [Acceder a la webCam con openCV y python](../Mostrar-la-webCam-o-reproducir-un-video-openCV-python/) y añado la función para ejecutar Canny. El código se muestra a continuación:

```python
import cv2

capture = cv2.VideoCapture(2)

while (capture.isOpened()):
    ret, frame = capture.read()
    if (ret == True):
        #Aplicar Canny a frame
        bordesCanny = cv2.Canny(frame, 100, 200)
        #Mostrar Ventanas
        cv2.imshow("Ventana", frame)
        cv2.imshow("Canny", bordesCanny)

        if (cv2.waitKey(1) == ord('s')):
            break
    else:
        break

capture.release()
cv2.destroyAllWindows()
```
En *Gif 1* se muestra la información de la cámara y el resultado de Canny detectando bordes.

![canny2](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1628206274/kipunaEC/canny/canny_ogs3mj.gif)
_Gif 1. Izq. Cámara, Der. Canny_

En el siguiente código añado un [filtro blur](https://docs.opencv.org/4.5.2/d4/d13/tutorial_py_filtering.html) antes de aplicar Canny y el resultado es que el filtro suaviza la imagen y se muestran menos contornos pequeños no deseados *Gif 2* 

![canny22](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1628205958/kipunaEC/canny/cannyBlur_cz6xqm.gif)
_Gif 2. Izq. Cámara. Der. Blur + Canny_

```python
import cv2

capture = cv2.VideoCapture(2)

while (capture.isOpened()):
    ret, frame = capture.read()
    if (ret == True):
        #Aplicar blur a frame
        blur = cv2.blur(frame, (5, 5))
        #Aplicar Canny a frame
        bordesCanny = cv2.Canny(frame, 100, 200)
        CannyBlur = cv2.Canny(blur, 100, 200)
        
        #Mostrar Ventanas
        cv2.imshow("Ventana", frame)
        cv2.imshow("Canny", bordesCanny)
        cv2.imshow("CannyBlur", CannyBlur)

        if (cv2.waitKey(1) == ord('s')):
            break
    else:
        break

capture.release()
cv2.destroyAllWindows()
```
***
## video

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/950oG9d0C44" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

*** 

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: OpenCV documentación. *Canny Edge Detection*. [https://docs.opencv.org/3.4/da/d22/tutorial_py_canny.html](https://docs.opencv.org/3.4/da/d22/tutorial_py_canny.html)
