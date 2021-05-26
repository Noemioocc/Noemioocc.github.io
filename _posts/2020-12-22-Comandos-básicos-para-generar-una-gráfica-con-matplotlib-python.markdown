---
title: Comandos básicos para generar una gráfica con matplotlib - python 
date: 2021-01-17 00:01:00 +0300
categories: [Python, Matplotlib ]
tags: [python, numpy, matplotlib, gráficos, legend, suptitle, tightlayout ]     
math: true
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_600/v1610906649/kipunaEC/python-matplot-b%C3%A1sico/matplotlib0_ocehw0.gif
---

***

## Matplotlib 

[**Matplotlib**](https://matplotlib.org/index.html) es una librería para [**python**](https://www.python.org/) que grafica datos en figuras con uno o más ejes.  

***

## Graficar funciones en matplotlib y python **.plot**

En este post registro como graficar pares ordenados `y1` y funciones `y2, y3, y4, y5, y6`.

$$
\begin{align*} 
&  y_1 \rightarrow Tab1        \\
\\
&  y_2 = -30          \\
\\
&  y_3 = cos (x)          \\
\\
&  y_4 = x^2 +100     \\
\\
&  y_5 = x^3 + 150    \\
\\
&  y_6 = x^3 + x^2 +200
\end{align*}
$$

#### Tab1. Pares ordenados de y1

| **x** 	|	0	|	1	|	2	|	3	|	4	|	5	|	
| **y**	|	70	|	30	|	30	|	70	|	70	|	70	|

Fig1. muestra seis funciones en un mismo gráfico con etiquetas en los ejes, títulos, rejillas, estilos y colores de línea establecidas por defecto [^por-defecto], más adelante registro como personalizar la gráfica. 

![Funciones](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_550/v1610907914/kipunaEC/python-matplot-b%C3%A1sico/matplotlib1_skfvil.jpg)
_Fig 1. Funciones constantes, trigonométrica, polinómicas en una misma gráfica_

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>

En los siguientes ítems describo el código que generó Fig1.
1. importar librerías/paquetes
 * [**Matplotlib**](https://matplotlib.org/index.html) paquete de trazado de python
 * [**Numpy**](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html) librería fundamental para cálculo de matrices con python
2. En cada función defino un dominio y un rango diferente. 
 * Para definir los **dominios** uso funciones de python como [arange](https://numpy.org/doc/stable/reference/generated/numpy.arange.html), [ones](https://numpy.org/doc/stable/reference/generated/numpy.ones.html) y [linspace](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html)
 * *Nota: Para evitar errores en el código la cantidad de puntos definido en en dominio `x` debe ser la misma cantidad que el rango `y`*
3. Usar función [.plot](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.plot.html) para graficar la figura
 * `plt.plot(x, y, label = "Texto")`, el primer y segundo agumento son los valores de `x, y` respectivamente. Tercer argumento `label` etiqueta cada función con un texto.
 * Junto con `label` se usa [legend](https://matplotlib.org/3.1.1/api/legend_api.html) y `loc`, en [**Tab2.**](#tab2-parámetros-permitidos-en-loc) estan los parámetros para ubicar el texto en una posición específica.
4. Funciones [title](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.title.html), [xlabel](https://matplotlib.org/3.3.2/api/_as_gen/matplotlib.pyplot.xlabel.html), [ylabel](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.ylabel.html) y [grid](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.grid.html) se mostrarán en Fig1 con valores por defecto.

</details>
{::options parse_block_html="false" /} 

```python
#Importar librerías
import numpy as np
import matplotlib.pyplot as plt
#Dominio y rango de cada función
x1 = [0,1,2,3,4,5]
y1 = [70,30,30,70,70,70]

x2 = np.arange(0,5, 0.15)
y2 = -30 * np.ones(len(x2))

x3 = np.arange(0,5/3.14*np.pi, 0.25)
y3 = 10*np.cos(2*x3)

x4 = np.linspace(0,5, 20, endpoint = True)
y4 = x4**2 + 100

x5 = np.arange(0,5, 0.1)
y5 = x5**3 + 150

x6 = np.arange(0,5, 0.8)
y6 = x6**3+x6**2+200
#Etiquetar cada función
plt.plot(x1, y1, label = "$y_1 -> Tab1$" )
plt.plot(x2, y2, label = "$y_2 = -30$")
plt.plot(x3, y3, label = "$y_3 = cos(x)$")
plt.plot(x4, y4, label = "$y_4 = x^2 +100$")
plt.plot(x5, y5, label = "$y_5 = x^3+150$")
plt.plot(x6, y6, label = "$y_6 = x^3+x^2+200$")
#Establecer la ubicación de cada leyenda
plt.legend(loc=1)
#Título, etiquetas en los ejes y malla
plt.title ('Colores y estilo de línea por defecto')
plt.xlabel("x")
plt.ylabel("y")
plt.grid()
#Guardar imagen en formato .jpg
plt.savefig("Funciones.jpg")
#Mostrar imagen
plt.show()                         
```

#### Tab2. Parámetros permitidos en loc

| loc =`'best'`  	| loc = 0		|
| loc =`'upper right'` | loc = 1		|
| loc =`'upper left'` 	| loc = 2  		|
| loc =`'lower left'`  | loc = 3 		|
| loc =`'lower right'` | loc = 4		|
| loc =`'right'` 	| loc = 5		|
| loc =`'center left'` | loc = 6  		|
| loc =`'center right'`| loc = 7 		|
| loc =`'lower center'`| loc = 8		|
| loc =`'upper center'`| loc = 9  		|
| loc =`'center '`  	| loc = 10 		|

***
## Markers, colores y fontsize en matplotlib **label**, **legend**, **fontsize** 

En este ejemplo uso [marcadores y colores](https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.plot.html) para graficar, Fig2 tiene las mismas funciones `y1, y2, y3, y4, y5, y6` que Fig1 pero con las siguientes características adicionales
 - Funciones graficadas con marcadores
 - Cambio el [color](https://matplotlib.org/3.1.0/gallery/color/named_colors.html) de la ecuación `y6`a magenta.
 - Uso`fontsize` para cambiar el tamaño del título y los ejes.

![Markers](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_550/v1610505084/kipunaEC/python-matplot-b%C3%A1sico/matplotlib2_rpjdak.jpg)
_Fig 2. Gráfico con marcadores_

El espaciado de los marcadores en las funciones de Fig2. se ve diferente en cada una, porque al definir los dominios con las funciones [arange](https://numpy.org/doc/stable/reference/generated/numpy.arange.html), [ones](https://numpy.org/doc/stable/reference/generated/numpy.ones.html) y [linspace](https://numpy.org/doc/stable/reference/generated/numpy.linspace.html) las muestras en cada arreglo son distintas. El código a continuación es el que generó Fig2. 

```python
#Importar librerías
import numpy as np
import matplotlib.pyplot as plt
#Dominio y rango de cada función
x1 = [0,1,2,3,4,5]
y1 = [70,30,30,70,70,70]

x2 = np.arange(0,5, 0.15)
y2 = -30 * np.ones(len(x2))

x3 = np.arange(0,5/3.14*np.pi, 0.25)
y3 = 10*np.cos(2*x3)

x4 = np.linspace(0,5, 20, endpoint = True)
y4 = x4**2 + 100

x5 = np.arange(0,5, 0.1)
y5 = x5**3 + 150

x6 = np.arange(0,5, 0.8)
y6 = x6**3+x6**2+200
#Etiquetar cada función
plt.plot(x1, y1,'o', label = "$y_1 -> Tab1$")
plt.plot(x2, y2,'v', label = "$y_2 = -30$")
plt.plot(x3, y3,'p', label = "$y_3 = cos(x)$")
plt.plot(x4, y4,'P',  label = "$y_4 = x^2 +100$")
plt.plot(x5, y5,'+',  label = "$y_5 = x^3+150$")
plt.plot(x6, y6, '1', color = 'm', label = "$y_6 = x^3+x^2+200$")
#Establecer la ubicación de cada leyenda
plt.legend(loc=1)
#Título, etiquetas en los ejes y malla
plt.title ('Establecer marcadores en una figura', fontsize= 15)
plt.xlabel("x", fontsize=20)
plt.ylabel("y", fontsize=20)

plt.grid()
#Guardar imagen en formato .jpg
plt.savefig("Funciones.jpg")
#Mostrar imagen
plt.show()                       
```

***

## Estilos de línea matplotlib

Para cambiar el tipo de línea, se debe agregar en la función `.plot` el *argumento de estilo* [**Tab4.**](#tab4-estilos-de-línea) 

#### Tab4. Estilos de línea		

| `'-'`  |  línea sólida	|
| `'--'` |  línea discontinua	|
| `'-.'` |  línea de puntos	|
| `':'`  |  linea punteada	|

```python
plt.plot(variableX, variableY,'Estilo de línea')
```
El argumento de estilo se puede combinar con los marcadores y el color, como el formato que tiene `y1, y2`. 

```python
plt.plot(x1, y1,'r--o', label = "$y_1 -> Tab1$")
plt.plot(x2, y2,'b-v', label = "$y_2 = -30$")
```

Para graficar líneas continuas y sin marcadores se debe usar el formato de `y4, y5, y6`.

```python
plt.plot(x4, y4,'-',  label = "$y_4 = x^2 +100$")
plt.plot(x5, y5,'--',  label = "$y_5 = x^3+150$")
plt.plot(x6, y6, '-.', color = 'm', label = "$y_6 = x^3+x^2+200$")
```

![Lineas](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_550/v1610507518/kipunaEC/python-matplot-b%C3%A1sico/matplotlib3_ggb3dt.jpg)
_Fig 3. Estilos de línea_

El siguiente código es el que generó Fig3.
```python
#Importar librerías
import numpy as np
import matplotlib.pyplot as plt
#Dominio y rango de cada función
x1 = [0,1,2,3,4,5]
y1 = [70,30,30,70,70,70]

x2 = np.arange(0,5, 0.15)
y2 = -30 * np.ones(len(x2))

x3 = np.arange(0,5/3.14*np.pi, 0.25)
y3 = 10*np.cos(2*x3)

x4 = np.linspace(0,5, 20, endpoint = True)
y4 = x4**2 + 100

x5 = np.arange(0,5, 0.1)
y5 = x5**3 + 150

x6 = np.arange(0,5, 0.8)
y6 = x6**3+x6**2+200
#Etiquetar cada función
plt.plot(x1, y1,'r--o', label = "$y_1 -> Tab1$")
plt.plot(x2, y2,'b-v', label = "$y_2 = -30$")
plt.plot(x3, y3,':p', label = "$y_3 = cos(x)$")
plt.plot(x4, y4,'-',  label = "$y_4 = x^2 +100$")
plt.plot(x5, y5,'--',  label = "$y_5 = x^3+150$")
plt.plot(x6, y6, '-.', color = 'm', label = "$y_6 = x^3+x^2+200$")
#Establecer la ubicación de cada leyenda
plt.legend(loc=1)
#Título, etiquetas en los ejes y malla
plt.title ('Tipos de línea y cambio de color', color = 'brown', fontsize= 15)
plt.xlabel("x", fontsize=20, color = 'teal' )
plt.ylabel("y", fontsize=20, color = 'teal')

plt.grid()
#Guardar imagen en formato .jpg
plt.savefig("Funciones.jpg")
#Mostrar imagen
plt.show()
```

***

## Subplots matplotlib python **fig**, **ax**
[Subplots](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.subplots.html) crea un conjunto figuras en un mismo gráfico sin solaparse. En este ejemplo uso las funciones establecidas a inicio del post `y1, y2, y3, y4`. 

![Lineas](https://res.cloudinary.com/dxh1bpaim/image/upload/v1610852282/kipunaEC/python-matplot-b%C3%A1sico/matplotlib4_gikds4.jpg)
_Fig 4. Sub imágenes. Funciones constantes, trigonométrica, polinómicas_

{::options parse_block_html="true" /}

<details>
<summary markdown='span'> Explicación detallada del código a continuación **Clic para desplegar** 
</summary>


La función `subplots` devuelve dos argumentos [fig, ax](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.subplots.html) 
`fig, ax = plt.subplots(2,2)`. Establezco `subplots`como una matriz de 2x2, que representan las posiciones de las figuras en el gráfico.
1. En **fig** uso funciones para dar formato a la figura (gráfica) en conjunto, como:
 * [suptitle](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.suptitle.html), etiqueto el título de la figura `'Ejemplo de funciones en un mismo gráfico Python - Matplotlib'`.
 * [text](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.text.html), etiqueto los ejes comunes de las figuras `'Eje común X', 'Eje común Y'`.
 * [tight_layout](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.tight_layout.html) ajusta automáticamente las figuras para rellenar proporcionalmente el espacio.
2. En **ax** uso funciones para dar formato a las sub figuras. como: 
 * [set_xlabel](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.axes.Axes.set_xlabel.html) establece una leyenda en el x.
 * [set_ylabel](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.axes.Axes.set_ylabel.html) establece una leyenda en el y.
 * [legend](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.legend.html) ubica lo que `label` contiene en una posción espcecifica [**Tab2.**](#tab2-parámetros-permitidos-en-loc).
 * [set_title](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.axes.Axes.set_title.html) escribe el título de cada sub figura.
 * [grid](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.grid.html), dibuja la malla.
 * *Nota: En* **ax** *se debe  especificar las pociciones* así `ax[0,1]`.
 
 </details>
{::options parse_block_html="false" /} 

```python
#Importar librerías
import numpy as np
import matplotlib.pyplot as plt

#Tupla (fig, ax)
fig, ax = plt.subplots(2,2)

#Seis funciones
x1 = [0,1,2,3,4,5]
y1 = [70,30,30,70,70,70]

x2 = np.arange(0,5, 0.15)
y2 = -30 * np.ones(len(x2))

x3 = np.arange(0,5/3.14*np.pi, 0.25)
y3 = 10*np.cos(2*x3)

x4 = np.linspace(0,5, 20, endpoint = True)
y4 = x4**2 + 100


#Función y1
ax[0,0].plot(x1, y1, 'r--o', label = "$y_1 -> Tab1$")
ax[0,0].set_xlabel('x', color = 'red',fontsize=12)
ax[0,0].set_ylabel('y', color = 'red',fontsize=12)
ax[0,0].legend(loc=1)
ax[0,0].set_title('y1')
ax[0,0].grid(color='powderblue', linestyle='--')

#Función y2
ax[0,1].plot(x2, y2, 'b-v', label = "$y_2 = -30$")
ax[0,1].set_xlabel('x', color = 'blue',fontsize=12)
ax[0,1].set_ylabel('y', color = 'blue',fontsize=12)
ax[0,1].legend(loc=1)
ax[0,1].set_title('y2')
ax[0,1].grid(color='powderblue', linestyle='--')

#Función y3
ax[1,0].plot(x3, y3, ':p', color = 'orange', label = "$y_3 = cos(x)$")
ax[1,0].set_xlabel('x', color = 'orange',fontsize=12)
ax[1,0].set_ylabel('y', color = 'orange',fontsize=12)
ax[1,0].legend(loc=1)
ax[1,0].set_title('y3')
ax[1,0].grid(color='powderblue', linestyle='--')

#Función y4
ax[1,1].plot(x4, y4, 'c-',  label = "$y_4 = x^2 +100$")
ax[1,1].set_xlabel('x', color = 'cyan',fontsize=12)
ax[1,1].set_ylabel('y', color = 'cyan',fontsize=12)
ax[1,1].legend(loc=1)
ax[1,1].set_title('y4')
ax[1,1].grid(color='powderblue', linestyle='--')

#Título de toda la figura
fig.suptitle('Ejemplo de funciones en un mismo gráfico Python - Matplotlib', fontsize=15)

#Nombres de ejes comunes
fig.text(0.5, 0.03, 'Eje común X', va='center', ha='center', fontsize=16)
fig.text(0.03, 0.5, 'Eje común Y', va='center', ha='center', fontsize=16, rotation='vertical')

#Evita solapamiento de textos
fig.tight_layout()

#Mostrar imagen
plt.show()
```
***

### Graficar tres funciones matplotlib **fig, ax = plt.subplots(3)**

En este ejemplo uso las funciones `y1, y2, y3` en un gráfico de 3x1, a diferencia del ejemplo anterior, las funciones en **ax** se usa como una matriz de una dimensión `ax[0]`, `ax[1]` y `ax[2]`. 

![Lineas](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,h_600,w_1000/v1610906812/kipunaEC/python-matplot-b%C3%A1sico/matplotlib5_letxob.jpg)
_Fig 5. Sub imágenes con funciones_

```python
#Importar librerías
import numpy as np
import matplotlib.pyplot as plt

#Tupla (fig, ax)
fig, ax = plt.subplots(3)

#Seis funciones
x1 = [0,1,2,3,4,5]
y1 = [70,30,30,70,70,70]

x2 = np.arange(0,5, 0.15)
y2 = -30 * np.ones(len(x2))

x3 = np.arange(0,5/3.14*np.pi, 0.25)
y3 = 10*np.cos(2*x3)

#Función y1
ax[0].plot(x1, y1, 'r--o', label = "$y_1 -> Tab1$")
ax[0].set_xlabel('x', color = 'red',fontsize=12)
ax[0].set_ylabel('y', color = 'red',fontsize=12)
ax[0].legend(loc=1)
ax[0].set_title('y1')
ax[0].grid(color='powderblue', linestyle='--')

#Función y2
ax[1].plot(x2, y2, 'b-v', label = "$y_2 = -30$")
ax[1].set_xlabel('x', color = 'blue',fontsize=12)
ax[1].set_ylabel('y', color = 'blue',fontsize=12)
ax[1].legend(loc=1)
ax[1].set_title('y2')
ax[1].grid(color='powderblue', linestyle='--')

#Función y3
ax[2].plot(x3, y3, ':p', color = 'orange', label = "$y_3 = cos(x)$")
ax[2].set_xlabel('x', color = 'orange',fontsize=12)
ax[2].set_ylabel('y', color = 'orange',fontsize=12)
ax[2].legend(loc=1)
ax[2].set_title('y3')
ax[2].grid(color='powderblue', linestyle='--')

#Título de toda la figura
fig.suptitle('Ejemplo de funciones en un mismo gráfico Python - Matplotlib', fontsize=15)

#Nombres de ejes comunes
fig.text(0.5, 0.03, 'Eje común X', va='center', ha='center', fontsize=16)
fig.text(0.03, 0.5, 'Eje común Y', va='center', ha='center', fontsize=16, rotation='vertical')

#Evita solapamiento de textos
fig.tight_layout()

plt.show()
```

***

> Aprendan siempre, aprendan mucho — Mimi

***

## Referencias

[^por-defecto]: **Por defecto** opción disponible si no se especifica lo contrario 

