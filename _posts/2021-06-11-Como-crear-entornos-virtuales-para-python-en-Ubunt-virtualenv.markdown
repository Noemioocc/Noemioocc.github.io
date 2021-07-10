---
title: Entornos virtuales para python en Ubuntu - virtualenv 
date: 2021-05-26 00:01:00 +0300
categories: [Python, Entornos Virtuales ]
tags: [python, openCV, terminal, pip, ubuntu, virtualenv]   
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625800348/kipunaEC/entornos/1_c1vbxt.png
---

***

# Entornos virtuales

Las aplicaciones en Python usualmente hacen uso de paquetes y módulos que no forman parte de la librería estándar y a veces necesitan una versión específica de una librería [^1]. Instalar y desintalar varias versiones de python o librerías se convertirá en una tarea extensa. Ahí entran los entornos virtuales al rescate.

Puedo crear varios entornos virtuales y en cada uno de ellos tener versiones de python distintas y tambien diferentes librerías.

En este post crearé un entorno virtual para python en Ubuntu. Usaré las herramienta **virtualenv**.

*Nota: También se puede crear entornos virtuales con venv, conda, pycharm, etc.*

***
# Entorno virtual con **virtualenv**
## 1. Verificar que **python**, **pip**, y **virtualenv** esten instalados

* [virtualenv](https://virtualenv.pypa.io/en/latest/) es una herramienta para crear entornos Python aislados. 

* [pip](https://pypi.org/project/pip/) es un instalador de paquetes para Python. A travez de `pip` puedo instalar dentro de un entorno virtual librerías como openCV, pandas, imageio, matplotlib, pillow, etc. *Nota: Las versiones más recientes de python ya viene con `pip` instalado*

Es probable que ya tengas instalado `python`, `pip` y `virtualenv` en ubuntu, así que primero verifico que esten instalados. Escribo en la terminal de `Ubuntu` los siguientes comandos y aparecerán las versiones instaladas.

*Nota: en mi computadora tengo instalado python3, asi que estos ejemplos los realizaré con esa version de python*

```terminal
python3 --version
```
```terminal
pip --version
```
```terminal
virtualenv --version
```
![versiones](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625760240/kipunaEC/entornos/versiones_lrjaum.png)
_Fig 1. Verificar la instalación de python, pip y virtualenv_

Si no está instalado `virtualenv` con el siguiente comando se puede realizar la instalación desde la terminal de `ubuntu`.

```terminal
pip install virtualenv
```

![instalar](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625762271/kipunaEC/entornos/virtualenvInstall_xharrx.png)
_Fig 2. Instalar virtualenv_


## 2. Crear un entorno virtual con virtualenv
* Crearé los entornos virtuales de este post en el `Escritorio` de `Ubuntu` en una carpeta llamada `EjemploEntornos`.
* Desde la terminal me ubico en la dirección `/Escritorio/EjemploEntornos` con el comandos `cd`. *También puede revisar [guía de comandos Ubuntu](https://www.guia-ubuntu.com/index.php/Comandos)*

Con el siguiente código en la terminal creo el entorno virtual llamado `MiEntorno1`

```terminal
virtualenv MiEntorno1
```

![mientorno1](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625763290/kipunaEC/entornos/miEntorno1_nan0tl.png)
_Fig 3. Crear entorno virtual llamado "MiEntorno1"_

Y verifico que dentro de "MiEntorno1" se crearon varios archivos.

![mientorno1carpetas](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625763445/kipunaEC/entornos/mientorno1carpeta_rgehmy.png)
_Fig 4. Carpetas que se crearon en "MiEntorno1"_

## 3. Activar un entorno virtual - virtualenv
* Para activar el entorno virtual debo acceder a la carpeta `bin` que se muestra en *Fig 4*.

Desde la terminal y con ayuda del comando `ls` y `cd` accedo a la carpeta `bin` como se muestra en  *Fig 5*. Una vez ubicados en la carpeta `bin` escribo lo siguiente en la terminal:

```terminal
source activate
```

![mientorno1cd](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625764595/kipunaEC/entornos/activarMientornook_i4b3vf.png)
_Fig 5. Activar "MiEntorno1"_

En *Fig 5* se observa que después de escribir `source activate` apareció el nombre del entorno entre paréntesis `(miEntorno1)` antes del nombre de usuario en la terminal, esto indica que el entorno virtual esta activo. 

* Otra forma de activar el entorno es escribiendo directamente en la terminal:

```terminal
source miEntorno1/bin/activate
```

![mientorno1terminal](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625764094/kipunaEC/entornos/activarmiEntorno1_sesipu.png)
_Fig 6. Activar "miEntorno1"_

## 4. El entorno activado

Siempre que se muestre el nombre del entorno `(miEntorno1)` estará activo. Y con el entorno activado puedo regresar al `Escritorio`, abrir otras carpetas, crear nuevas carpetas, crear scripts, etc. 

*Nota: No necesariemente debo estar ubicada donde creé el entorno "miEntorno1" para crear los scripts de python.*

Con el comando `cd` salgo de la carpeta donde estaba creado el entorno, como se ve en *Fig 7*. 

![mientorno1terminal](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625767176/kipunaEC/entornos/cdEscritorioentorno_zcoeuy.png)
_Fig 7. Entorno activado_
 
## 5. Instalar paquetes con pip en el entorno virtual
En este ejempo instalaré openCV y matplotlib a travéz de [pip](https://pypi.org/project/pip/):
* OpenCV (la última versión disponible)

```terminal
pip install opencv-python 
```
![openCV](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625769939/kipunaEC/entornos/python-openCV_q4anko.png)
_Fig 8. Instalando opencV_


* Matplotlib versión 3.3.2

```terminal
pip install matplotlib==3.3.2
```

![matpplotlib](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625769941/kipunaEC/entornos/matplotlib_r9kpuj.png)
_Fig 9. Instalando Matplotlib_


Se puede encontrar en la página de [pip](https://pypi.org/project/pip/) muchas librerías con sus respectivas versiones nuevas y antiguas.

## 6. Verificar las librerías instaladas en un entorno

Para eso uso la función `freeze` y escribo en la terminal

```terminal
pip freeze
```

![matplotlib](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625770169/kipunaEC/entornos/freeze_gudv3u.png)
_Fig 9. Listado de librerías instaladas_

## 7. Ejecutar un script en el entorno virtual

En el `Escritorio` tengo un script de python llamado `mostrarImagen.py`, este script muestra varias imágenes usando openCV y Matplotlib, este código esta disponibe en github [Mostra imágenes Matplotlib](https://github.com/kipunaEc/Python-OpenCV-Mostrar-Imagenes-Matplotlib). 

Con el entorno activado, uso los comandos `cd` y `ls` para moverme hacia la dirección del script. `/home/noemi/Escritorio/`, y [ejecuto el script python desde la terminal](../Cómo-ejecutar-un-script-python-desde-la-terminal/)

![matplotlib](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625773765/kipunaEC/entornos/script_qiwiok.png)
_Fig 10. Ejecutar script desde el entorno virtual_

## 8. Desintalar una librería del entorno

Para desintalar una librería del entorno se debe usar la palabra `uninstall` seguido del nombre con el que se instaló la librería, como se muestra a continuación, desintalaré `opencv-python`:

```terminal
pip uninstall opencv-python
```

*Nota: Si la librería tiene una versión específica se debe añadir en el nombre, al igual que la monmento de instalar*

## 9. Migrar un entorno virtual - virtualenv
Para migrar un entorno debo crear un archivo llamado `requirements.txt` en este archivo se mostrará todas las librerías que se instalaron en un entorno determinado.

Escribo en la terminal

```terminal
pip freeze > requirements.txt
```
![requirements](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625890442/kipunaEC/entornos/requirements_e9qbva.png)
_Fig 11. Comando para crear el archivo requirements.txt_

El archivo `requirements.txt` contiene la siguiente información que son las librerías instaladas en `miEntorno1` (Para este ejemplo)
```
certifi==2021.5.30
cycler==0.10.0
kiwisolver==1.3.1
matplotlib==3.3.2
numpy==1.21.0
opencv-python==4.5.2.54
Pillow==8.3.1
pyparsing==2.4.7
python-dateutil==2.8.1
six==1.16.0
```

Finalmente, para migrar el entorno virtual con las mismas librerias que estan en `requirements.txt`, primero copio el archivo `requirements.txt` en el nuevo entorno virtual `miEntorno3`, como se indica en *Fig 12.*

![requirementstxt](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625891097/kipunaEC/entornos/copiorequirremenst_xathuj.png)
_Fig 12. Archivo requirements.txt copiado en el nuevo entorno_

Con el nuevo entorno creado y el archivo `requirements.txt` en la misma carpeta, ejecuto el siguiente comando:


```terminal
pip install -r requirements.txt
```

![requirementstxt](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625891549/kipunaEC/entornos/requiremenstInstallok_dldpij.png)
_Fig 13. Instalar librerías de requirements.txt_


## 10. Desactivar el entorno virtual

Para desacivar el entorno virtual, basta con escribir `deactivate`en la terminal.

```terminal
deactivate
```
![deactivate](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1000/v1625775013/kipunaEC/entornos/deactivate_suwvms.png)
_Fig 11. Desactivar entorno virtual_


Se pueden craer tantos entornos virtuales como necesites, con diferentes librerías y versiones cada uno. Así como también se puede encontrar más aplicaciones a los entornos. 


*** 

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: OpenCV. *Creación de entornos virtuales*. disponible en: [https://docs.python.org/es/3/tutorial/venv.html](https://docs.python.org/es/3/tutorial/venv.html)

