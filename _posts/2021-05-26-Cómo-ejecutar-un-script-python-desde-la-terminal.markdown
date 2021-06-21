---
title: Cómo ejecutar un script desde la terminal de Ubuntu
date: 2021-05-26 00:01:00 +0300
categories: [Python, openCV ]
tags: [python, openCV, terminal, pip, ubuntu]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1622045279/kipunaEC/ejecutarTerminal/portada_kr4sfd.png
---

***

En este post realizaré 3 ejemplos, un script de python, un script con la librería openCV (ya instalada en Ubuntu) y un script con la librería imageio (instalaré con `pip`)

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/6AMsTkPCQGI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

***

## **Ejecutar un script python (Ejemplo 1)**
#### 1. Abro la terminal de Ubuntu

![terminal](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622034754/kipunaEC/ejecutarTerminal/termial_kijhwa.png)
_Fig 1. Terminal de Ubuntu abierta_

### 2. Revisar que **python** este instalado 

Para python2
```terminal
python2 --version
```
Para python3
```terminal
python3 --version
```

![versionespython](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622035252/kipunaEC/ejecutarTerminal/pythonversion_wla7ie.png)
_Fig 2. Revisar la versión de python_


### 3. Abrir la ubicación donde se encuentre el script

Mi script se llama `comparacion.py` 
```python
print('Me gusta python')

A = 25
B = 50

if (A < B):
	print('A es menor que B')
else:
	print('A es mayor que B')	
```

Y esta en la dirección `/home/noemi/Escritorio/script1-python`. Con los [comandos](https://www.guia-ubuntu.com/index.php/Comandos) de la terminal de Ubuntu como  `cd`  me muevo hasta llegar a la ubicación

```terminal
noemi@noemi:~$ cd Escritorio
noemi@noemi:~/Escritorio$ cd script1-python
```

![terminalcomandos](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622044588/kipunaEC/ejecutarTerminal/abrirdireciion_jdezu6.png)
_Fig 3. Abrir la dirección del script en una terminal_


O tambien puedo ubicarme en la carpeta que contiene el script y con clic derecho seleccionar `abrir en una terminal`

![terminalCArpeta](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622044364/kipunaEC/ejecutarTerminal/carpetaterminal_wivswh.png)
_Fig 4. Abrir la dirección del script en una terminal_

### 4. Ejecutar el script
Si la terminal esta abierta en la ubicacion que contiene el archivo, para ejecutarla (con python3) se escribe `python3` y adjunto el nombre del script y su extensión `.py`

```terminal
python3 comparacion.py
```
![ejecutar](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622044960/kipunaEC/ejecutarTerminal/ejecutar_hrjpkh.png)
_Fig 5. Scrt ejecutado_

***

## **Ejecutar un script python - openCV (Ejemplo 2)**
### 1. Verifico que python y openCV estan instalados
Escribo `python3` en la terminal para que se abra python directamente.

```terminal
python3
```
Cuando python3 este funcionando en la terminal escribo
```terminal
cv2.import cv2
cv2.__version__
```
*Nota: Escribo exit() para salir de python en la terminal*

![versionopenCV](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622045741/kipunaEC/ejecutarTerminal/versionopenCV_dwp0jf.png)
_Fig 6. Revisar la versión de openCV_

### 2. Abro la direccion del script en la terminal 

El script que voy a ejecutar se llama `mostrarImagen.py` y abre la imagen `galapagos.jpg` con la librería [openCV](https://opencv.org/)

*Imagen usada para ejecutar el script: 'Galapagos sea lion napping on a bench' by Jackman Chiu on Unsplash*

```python 
import cv2

img = cv2.imread('galapagos.jpg') 

cv2.imshow('Ventana', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

Igual que en el ejemplo anterior puedo abrir la ubicación desde la terminal con el [comando](https://www.guia-ubuntu.com/index.php/Comandos) `cd`, o ubicándome en la carpeta que contiene el script y seleccionado `abrir en una terminal`

![abrirterminal2](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622046127/kipunaEC/ejecutarTerminal/ejemplo2_itcjpa.png)
_Fig 7. Abrir la terminal donde esta el script y la imagen_

### 3. Ejecuto el programa
Escribo la siguiente línea de codigo que corresponde al nombre de mi script y aparece la imagen. 

```terminal
python3 mostrarImagen.py
```
*Imagen usada para ejecutar el script: 'Galapagos sea lion napping on a bench' by Jackman Chiu on Unsplash*

![abrirterminalej22](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622046418/kipunaEC/ejecutarTerminal/ejecutarej2_onmwdk.png)
_Fig 8. Ejecutar el script y se muestra la imagen_

***

## Ejecutar un script python - imageio (Ejemplo 3)
Este script crea un [gif a partir de imágenes](../Crear-un-gif-con-imagenes-imageio-python/) y está ubicado en la dirección `/home/noemi/Escritorio/script3-python-imageio`.
En este ejemplo NO tengo instalada la librería [imageio](https://pypi.org/project/imageio/), así que si ejecuto el programa va a aparecer un error. Así que primero debo instalar `imageio`
### 1. Instalo **imageio** con pip
Para instalar [imageio](https://pypi.org/project/imageio/) uso el instalador de paquetes [pip](https://pypi.org/project/pip/)

```terminal
pip install imageio
```

![instapimageio](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622047388/kipunaEC/ejecutarTerminal/1_dlovp2.png)
_Fig 9. Instalar imgeio con pip_

### 2. Abro la carpeta donde esta guardado el script
En la dirección del proyecto esta una carpeta que contiene las imágenes que uso para crear el gif y el archivo `crearGif.py`. Hago clic derecho dentro de la carpeta y selecciono `Abrir en una terminal`

![abrirterminale3](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622047183/kipunaEC/ejecutarTerminal/abrirejempl3_s6cof8.png)
_Fig 10. Abrir la ubicación del script en la terminal_


![abrirterminale3](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622048663/kipunaEC/ejecutarTerminal/termina5_s3nbqj.png)
_Fig 11. Abrir la ubicación del script en la terminal_


### 3. Ejecutar el programa
El nombre de mi script es `crearGif.py`entonces escribo

```terminal
python3 crearGif.py
```
Cuando el script se ejecuta, con el comando `ls` puedo ver que se ha creado el script.

*Nota: Para que el script 3 funcione correctamente se debe cambiar la dirección de las imagenes por su directorio local donde se encuentren*

![sdf](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1622047380/kipunaEC/ejecutarTerminal/3_ympnkp.png)
_Fig 12. Ejecutar el script y se crea el archivo .gif_


*** 

> Aprendan siempre, aprendan mucho — Mimi

***

