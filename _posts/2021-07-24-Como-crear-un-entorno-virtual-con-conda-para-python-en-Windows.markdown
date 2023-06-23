---
title: Entornos virtuales con conda en Windows
date: 2021-07-24 00:01:00 +0300
categories: [Python, Entornos Virtuales ]
tags: [python, openCV, cmd, conda, windows]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1628129174/kipunaEC/entornosWindows/conda_cteczl.png
redirect_to: https://kipunaec.com/entornos-virtuales-python-en-windows-virtualenv-y-conda/
---

***

# Hacer zoom en los píxeles openCV

Este post es el complemento de [crear una imagen con numpy y openCV](../Crear-una-imagen-BGR-openCV-Python/#video) porque en `Windows` algunos lectores registraron que no se puede hacer ZOOM y no se puede ver los valores de los píxeles de las imágenes como en este [video creado e Ubuntu](../Crear-una-imagen-BGR-openCV-Python/#video). Indagando por internet encontré que una solución para poder visualizar los valores de los píxeles es ejecutar el script python-openCV en un entorno virtual creado con conda [^1].

En el video al final del post muestro de manera práctica como crear entornos virtuales con viertualenv y con conda en Windows.

*Nota: También se puede crear entornos virtuales con venv,[virtualenv](../Como-crear-entornos-virtuales-para-python-en-Ubunt-virtualenv/), conda, etc.*

# Entorno virtual

Las aplicaciones en Python usualmente hacen uso de paquetes y módulos que no forman parte de la librería estándar y a veces necesitan una versión específica de una librería [^2]. Instalar y desinstalar varias versiones de python o librerías se convertirá en una tarea extensa. Ahí entran los entornos virtuales al rescate.

***
# Entorno virtual con **conda**
## 1. Instalar **python** y **Anaconda** 

Marco las casillas  **add to PATH** al instalar `python` y `Anaconda` para poder usar como variables de entorno en el `cmd`. En el [**video**](#video) al final de este post puedes revisar la instalación completa de `python` y `Anaconda`

* [python downloads](https://www.python.org/downloads/windows/) En la página oficial de python se encuentran varios versiones que se puede usar dependiendo la versión de Windows porque las versiones más actuales de python no funciona para windows 7 o xp. 
En esta parte de la instalación selecciono add to PATH

![pythonInstall](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_400/v1628128502/kipunaEC/entornosWindows/installpython_vbaf8w.png)
_Fig 1. Marcar **add to path** el instalar python en windows_

* [Anaconda downloads](https://docs.anaconda.com/anaconda/install/windows/), después de descargar el instalador, en esta parte selecciono add to PATH 

![AnacondaInstall](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_350/v1628128503/kipunaEC/entornosWindows/installAnaconda_smyw7i.png)
_Fig 2. Marcar add to path el instalar Anaconda en windows_

Es probable que ya tengas instalado `python` y `conda` en Windows, así que primero verifico que estén instalados. Escribo en el `cmd` de `Windows` los siguientes comandos y aparecerán las versiones instaladas.

```terminal
python --version
```
```terminal
conda --version
```

![versiones](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628128503/kipunaEC/entornosWindows/cmdVersion_r9fcul.png)
_Fig 3. Verificar la instalación de python, pip y virtualenv_


## 2. Crear un entorno virtual con conda en Windows
Conda guarda automáticamente todos los entornos virtuales dentro del directorio `envs` que está dentro de la instalación de Anaconda [^3]. (Si quieres guardar en otra carpeta puedes revisar esto: [How to specify new environment location for conda create](https://stackoverflow.com/questions/37926940/how-to-specify-new-environment-location-for-conda-create))

Con el siguiente código en la terminal creo el entorno virtual llamado `miEntorno1`

```terminal
conda create --name miEntorno1
```

![mientorno1](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628128503/kipunaEC/entornosWindows/condacreatemientorno1_z7g5at.png)
_Fig 4. Crear entorno virtual llamado "MiEntorno1"_

## 3. Activar un entorno virtual - conda
Para activar el entorno virtual debo escribir en el terminal el siguiente comando:

```terminal
conda activate miEntorno1
```

![mientorno1cd](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628128499/kipunaEC/entornosWindows/condaactivate_udzbea.png)
_Fig 5. Activar "MiEntorno1"_

Y después de activar el entorno aparece el nombre del entorno entre paréntesis `(miEntorno1)` antes del nombre de usuario en la terminal, esto indica que el entorno virtual esta activo. 

## 5. Instalar paquetes con conda 
En este ejemplo instalaré openCV y matplotlib a través de [conda](https://docs.conda.io/en/latest/):

* OpenCV (la última versión disponible)

```terminal
 conda install -c conda-forge opencv 
```
![openCV](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628128498/kipunaEC/entornosWindows/installopenCV_jin8uj.png)
_Fig 6. Instalando opencV_


* Matplotlib versión 3.3.2

```terminal
 conda install -c conda-forge matplotlib==3.3.2
```

![matpplotlib](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628128497/kipunaEC/entornosWindows/matplotlib_bfvsgl.png)
_Fig 9. Instalando Matplotlib versión 3.3.2_


## 6. Verificar las librerías instaladas en un entorno

Con el entorno activo escribo en la terminal:

```terminal
conda list
```

![list](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628130873/kipunaEC/entornosWindows/condalist_x2glg1.png)
_Fig 9. Listado de librerías instaladas_

## 7. Ejecutar un script en el entorno virtual

En el `Escritorio` tengo un script de python llamado `mostrarImagen.py`, este script muestra una imágen usando openCV.

Con el entorno activado, uso los comandos `cd` y `dir` en `Windows` para moverme hacia la dirección del script, y [ejecuto el script python desde la terminal](../Cómo-ejecutar-un-script-python-desde-la-terminal/) y ahora ya puedo hacer zoom sobre los pixeles de la imagen que se muestra con openCV.


## 9. Exportar un entorno virtual con conda
Para exportar un entorno debo crear un archivo llamado `enviroment.yaml` en este archivo se mostrará  el nombre del entorno y todas las librerías que se instalaron

Para crear el archivo `.yaml` escribo en la terminal:

```terminal
conda env export > enviroment.yaml
```
![enviroments](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628128498/kipunaEC/entornosWindows/enviromenyt_y1ztln.png)
_Fig 11. Comando para crear el archivo enviroment.yaml_

El archivo `enviroment.yaml` contiene la siguiente información que son las librerías instaladas en `miEntorno1` (Para este ejemplo)

![enviroments](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628130874/kipunaEC/entornosWindows/archivoyaml_xy4x0d.png)
_Fig 12. Comando para crear el archivo enviroment.yaml_


# Migrar un entorno conda

Con el archivo `enviroment.yaml` puedo migrar el entorno virtual, este archivo se puede mover a otras computadoras con conda instalado y se puede replicar el entorno virtual.

Desde el `cmd` con los comandos `cd` y `dir` me ubico en la carpeta que contiene el archivo `enviroment.yaml`, y después ejecutar el siguiente comando:

```terminal
conda env create -f enviroment.yaml
```
Y se creara un nuevo entorno virtual conda con el nombre que esta en el archivo `enviroment.yaml`. 

![requirementstxt](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628131482/kipunaEC/entornosWindows/createinstall_zq0cof.png)
_Fig 13. Crear un nuevo entorno desde el archivo enviroment.yaml_

En ese entono virtual nuevo, puedo revisar con `conda list` las librerías y tambien ya puedo ejecutar scripts.


## 10. Desactivar el entorno virtual

Para desactivar el entorno virtual, basta con escribir `deactivate`enn la terminal.

```terminal
deactivate
```
![deactivate](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1628128499/kipunaEC/entornosWindows/condaactivate_udzbea.png)
_Fig 11. Desactivar entorno virtual_


Se pueden crear tantos entornos virtuales como necesites, con diferentes librerías y versiones cada uno. 

## video

<div class="embed-container">

<iframe width="586" height="342" src="https://www.youtube.com/embed/hBOxyO5QTNA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

*** 

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: stackoverflow - respuesta: midjji. *Expanded GUI for openCV with python and conda*. Disponible en: [https://stackoverflow.com/questions/48788908/expanded-gui-for-opencv-with-python-and-conda](https://stackoverflow.com/questions/48788908/expanded-gui-for-opencv-with-python-and-conda)
[^2]: OpenCV. *Creación de entornos virtuales*. disponible en: [https://docs.python.org/es/3/tutorial/venv.html](https://docs.python.org/es/3/tutorial/venv.html)
[^3]: Ram'on Invarato (2020). *Entornos virtuales de Python: común y Anaconda *. Disponible en: [https://jarroba.com/entornos-virtuales-de-python-comun-y-anaconda/](https://jarroba.com/entornos-virtuales-de-python-comun-y-anaconda/)


