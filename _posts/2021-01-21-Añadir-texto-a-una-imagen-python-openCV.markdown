---
title: Añadir texto y formas a una imagen python openCV
date: 2021-01-21 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, texto, imagen]   
math: true
image: https://res.cloudinary.com/dxh1bpaim/image/upload/v1611325632/kipunaEC/imagen-texto/rucoTexto-min_jgsgs1.jpg
---

## Textos y formas en openCV python

![Texto-imagen](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_1934,w_2591/v1611325632/kipunaEC/imagen-texto/rucoTexto-min_jgsgs1.jpg){:.thumbnail.bordered, width= 10 }

<center>
<p style="color: rgb(199,207,210);"> Fig 1. Texto y flecha en una imagen - openCV </p>
</center>

## Texto en una imagen - **putText**

[putext](https://docs.opencv.org/master/d6/d6e/group__imgproc__draw.html#ga5126f47f883d730f633d74f07456c576) es una función de openCV que agrega texto en una posición, tipo, tamaño, color y grosor específicos. 

```python
cv2.putText(img, texto, ubicacion, font, tamañoLetra, colorLetra, grosorLetra, bottomLeftOrigin = False)
```

![Texto-imagen](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_1936,w_2591/v1611339416/kipunaEC/imagen-texto/Quito1_hqvwrt.jpg){:.thumbnail.bordered, width= 10 }

<center>
<p style="color: rgb(199,207,210);"> Fig 2. Texto en una imagen de dimensión (2592 x 1963) - openCV </p>
</center>
 
A continuación se describe el código que generó Fig2. 

1. `img` imagen donde se va a escribir el texto
2. `texto` cadena de caracteres que aparecerá en la imagen
3. `ubicacion` tiene dos coordenadas `ancho, alto` **Fig1. ancho = 2591, alto = 1936**
 * La posición `(0 , 0)`es la superior izquierda
 * La posición `(2592, 1936)` es la esquina inferior derecha
4. `font` tipo de letra disponible ver [**Tab1.**](#tab1-tipos-de-letra)
5. `tamañoLetra` es un entero que especifica que tan grande o pequeño se mostrará el texto
6. `colorLetra` se escribe en formato `BGR`
7. `grosorLetra` se muestra el texto más voluminoso
8. `bottomLeftOrigin` es opcional, 
 * `bottomLeftOrigin = False`
 * Por defecto es `False`y la posición `(0,0)` es la superior izquierda

```python
#Importar librería cv2
import cv2

#Leer imagen
img = cv2.imread('Quito.jpg')

#Características del texto
texto = "Quito"
ubicacion = (200,700)
font = cv2.FONT_HERSHEY_TRIPLEX
tamañoLetra = 25
colorLetra = (221,82,196)
grosorLetra = 10

#Escribir texto
cv2.putText(img, texto, ubicacion, font, tamañoLetra, colorLetra, grosorLetra)

#Guardar imagen
cv2.imwrite('textoQuito.jpg', img)

#Mostrar imagen
cv2.imshow('imagen',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### Tab1. Tipos de letra

 | cv2.FONT_HERSHEY_SIMPLEX = 0	|
 | cv2.FONT_HERSHEY_PLAIN = 1		|
 | cv2.FONT_HERSHEY_DUPLEX = 2	|	
 | cv2.FONT_HERSHEY_COMPLEX = 3	|
 | cv2.FONT_HERSHEY_TRIPLEX = 4	|
 | cv2.FONT_HERSHEY_COMPLEX_SMALL = 5	|
 | cv2.FONT_HERSHEY_SCRIPT_SIMPLEX = 6 |	
 | cv2.FONT_HERSHEY_SCRIPT_COMPLEX = 7 |	
 | cv2.FONT_ITALIC = 16		|	

## Formas en una imagen python - openCV 
### Crear un espacio `img` para dibujar formas

### **line()** openCV

[line](https://docs.opencv.org/master/d6/d6e/group__imgproc__draw.html#ga7078a9fae8c7e7d13d24dac2520ae4a2) es una función de openCV que dibuja una línea uniendo dos puntos. 

```python
import cv2

#Leer imagen
img = cv2.imread('Quito.jpg')

#Tipos de letra - Fuentes de texto
font0 = cv2.FONT_HERSHEY_SIMPLEX
font1 = cv2.FONT_HERSHEY_PLAIN
font2 = cv2.FONT_HERSHEY_DUPLEX
font3 = cv2.FONT_HERSHEY_COMPLEX
font4 = cv2.FONT_HERSHEY_TRIPLEX
font5 = cv2.FONT_HERSHEY_COMPLEX_SMALL
font6 = cv2.FONT_HERSHEY_SCRIPT_SIMPLEX
font7 = cv2.FONT_HERSHEY_SCRIPT_COMPLEX
font8 = cv2.FONT_ITALIC

#Bucle for, escribir 9 veces Quito
for i in range(9):
    print(i)
    #Tipo de letra
    tipoLetra = [font0,font1,font2,font3,font4,font5,font6,font7,font8]

    #Texto
    texto = "Quito"

    #Tamaño de letra
    tamañoLetra = 10

    #Color de letra BGR, cambia conforme cambia i
    colorLetra = (221-20*i, 256-15*i, 10+50*i)

    #Grosor de letra, camba a igual que i en multiplos de 4
    grosorLetra = 3*i

    #La ubicación mantiene en 100 el eje X (ancho)
    # y cambia en multiplos de 200 el eje Y (alto)
    ubicacion = (100,200+205*i)

    #Escribe el texto en la imagen
    cv2.putText(img, texto, ubicacion, tipoLetra[i], tamañoLetra, colorLetra, grosorLetra, cv2.LINE_AA)

#Guardar imagen
cv2.imwrite('Quito0.jpg', img)

#Mostrar imagen
cv2.imshow('Quito',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
``` 






```python
import cv2

#Leer imagen
img = cv2.imread('ruco.jpg')

#CAracterísticas de la flecha
puntoInicial = (700, 700)
puntoFinal = (1425, 1225)
colorFlecha = (221,82,196)
grosorFlecha = 40
tipoLinea = cv2.LINE_4

#Características del texto
texto1 = "Cumbre"
texto2 = " Ruco Pichincha"
ubicacion1 = (800,350)
ubicacion2 = (50,590)
font = cv2.FONT_HERSHEY_TRIPLEX
tamañoLetra = 8
colorLetra = (221,82,196)
grosorLetra = 5

#Graficar una flecha
cv2.arrowedLine(img, puntoInicial, puntoFinal, colorFlecha, grosorFlecha, tipoLinea)
#Escribir texto
cv2.putText(img, texto1, ubicacion1, font, tamañoLetra, colorLetra, grosorLetra, cv2.LINE_AA)
cv2.putText(img, texto2, ubicacion2, font, tamañoLetra, colorLetra, grosorLetra, cv2.LINE_AA)

#Guardar imagen
cv2.imwrite('rucoTexto.jpg', img)

#Mostrar imagen
cv2.imshow('imagen',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

