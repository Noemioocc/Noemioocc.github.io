---
title: Ejecutar un script python con argparse
date: 2021-12-07 00:01:00 +0300
categories: [Python, Python básico]
tags: [python, openCV, directorio, os, argparse, path, ubuntu]
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_640/v1642531710/kipunaEC/argparse/portadaArgs_jbshl7.gif
---

***
En este post detallo cómo ejecutar un script python con argumentos desde el cmd, usando [argparse](https://docs.python.org/3/library/argparse.html#module-argparse). Mostraré varios ejemplos para comprender el funcionamiento. 

# Argparse 
 El módulo `argparse` es parte de la biblioteca estandar python para analizar argumentos enviados desde la línea de comandos. `Argparse` es un analizador sintáctico, usaré el término **parser** para referirme al analizador sintáctico como muestra en su [documentación oficial](https://docs.python.org/es/dev/library/argparse.html#module-argparse).

![parser](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1639494131/kipunaEC/argparse/parser_vzfih7.gif)
_Gif 1. Documentación oficial python - PARSER_

# Argparse - python
Consideremos 4 puntos importantes para empezar a usar `argparse`
1. [Importar biblioteca](https://docs.python.org/es/dev/library/argparse.html#module-argparse): `import argparse`
2. [Crear un objeto de ArgumentParser](https://docs.python.org/es/dev/library/argparse.html#creating-a-parser) llamado **parser**: `parser = argparse.ArgumentParser()`
3. [Añadir argumentos](https://docs.python.org/es/dev/library/argparse.html#adding-arguments) a **parser**: `parser.add_argument()`
4. [Analizar argumentos](https://docs.python.org/3/library/argparse.html#parsing-arguments): `args = parser.parse_args()`

***Nota:*** *Los códigos en todo el post se ejecutan con* **python 3**

***

## Ejemplo1 - argparse
Este ejemplo1, imprime exactamente lo mismo que ingresas como argumento, igual que en **Gif 2** ¡Veámos como va!

![ejemplo1GIF](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_728/v1642538092/kipunaEC/argparse/ejemplo1_yrtn4s.gif)
_Gif 2. Imprimir el argumento ingresado_

```python
#importar la biblioteca
import argparse
#Crear objeto parse
parser = argparse.ArgumentParser()
#Añadir argumentos a parse
parser.add_argument("texto")
#Pasar los argumentos
args = parser.parse_args()
#Imprimir en el terminal el resultado
print(args.texto)
```
Guardo el anterior código con el nombre `ejemplo1.py` y en la terminal [ejecuto el script](../Cómo-ejecutar-un-script-python-desde-la-terminal/) añadiendo cualquier caracter o texto como augumento (mi texto es "Hola_kipuna"), así:

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo1.py Hola_kipuna
```

![ejemplo01](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1642538547/kipunaEC/argparse/Ejemplo1_cj28eh.png)
_Fig 1. Argumento ingresado Hola_kipuna, e imprime Hola_Kipuna_

**¡El ejemplo1 fue sencillo!**, pero `argparse` es mucho mas que eso :D

***
## Ejemplo2 - argparse

En este ejemplo2 añado dos argumentos en la linea de comandos (Tu nombre y un número para obtener el [valor al cuadrado](http://geogebra.es/cvg_primaria/05/html/cuadrado.html)), el resultado será una frase como muestra **Fig 2**. 

*Nota:* Mientras avance con los ejemplos iré añadiendo parámetros a el [método add_argument()](https://docs.python.org/es/dev/library/argparse.html#the-add-argument-method) como a continuación el *tipo de dato*

### Tipo de dato

Además de añadir un nuevo argumento `"x"` , especifico el [tipo de dato](https://docs.python.org/es/dev/library/argparse.html#type) (`type`) al que debe convertirse el argumento de la línea de comandos. 
* *nombre* es `str` 
* *x* es `float` 

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("nombre", type = str)
parser.add_argument("x", type = float)
args = parser.parse_args()

print('Hola,',args.nombre,'! El valor al cuadrado de', args.x, 'es', args.x**2 )
```
![ejemplo02](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_698/v1642539824/kipunaEC/argparse/Ejemplo2_yqrrat.png)
_Fig 2. Ingresan dos argumentos al script_

### Mensajes de ayuda

Con el mismo ejemplo2 agregaré un [mensaje de ayuda](https://docs.python.org/es/dev/library/argparse.html#help) que añade una descripción en el argumento. En cada `.add_argument` agrego el parámetro `help`.

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("nombre", type = str, help = 'Tu nombre')
parser.add_argument("x", type = float, help = 'Número para encontrar el cuadrado') 
args = parser.parse_args()

print('Hola,', args.nombre, '! el valor al cuadrado de', args.x, 'es', args.x**2 )
```
Con el mensaje de ayuda, se puede recordar que valores deben ingresar en la línes de comandos para que los argumentos tengan sentido y funcione el código. Para que aparezca la ayuda se debe escribir `-h` después del script , así:

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo2.py -h
```
El resultado será como se muestra en *Fig 3*:

![ayuda02](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_700/v1642540435/kipunaEC/argparse/Ejemplo22_ybsekc.png)
_Fig 3. Mensaje de Ayuda_

1. `Usage`: Muestra el nombre del script y los argumentos que puede recibir, en este ejemplo son: `-h` `nombre` `x`. Algunos son argumentos posicionales imprescindibles para funcionar como `nombre` y `x`; otros no como `-h` que es un argumento opcional.
2. `positional arguments`: Son argumentos que debe recibir el script para funcionar, junto se muestra una breve reseña de lo que recibe como argumento (`nombre` `x`).
3. `optional arguments`: Son opcionales, no son imprescindibles para funcionar como:`-h` que es la ayuda.

![argumentos](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_400/v1642542437/kipunaEC/argparse/argumentos-min_snyqxj.png)
_Fig 4. Argumentos opcionales y posicionales_

***

## Ejemplo3 - argparse
En este ejemplo se introducen varios argumentos numéricos y se suman entre ellos. También se introduce el parámetro `nargs` del [método add_argument()](https://docs.python.org/es/dev/library/argparse.html#the-add-argument-method)

### Número de argumentos en la linea de comandos - nargs

[nargs](https://docs.python.org/es/dev/library/argparse.html#nargs) asocia un número diferente de argumentos de línea de comandos con una sola acción. Los valores permitidos en [nargs](https://docs.python.org/es/dev/library/argparse.html#nargs) son:

* `N` se especificando un número entero ej: `nargs=6`
* `'*'` ingresan multiples argumentos y se recogen en una lista
* `'+'` ingresan multiples argumentos y se recogen en una lista igual que `'*'`, pero si no ingresa ningun argumento mostrará un mensaje de error.
* `'?'` ingresará un valor desde la linea de comandos si es posible


En el siguiente código especifico `nargs` como `nargs=6`, imprimo los enteros que ingresan y sumo esos valores.
```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('enteros', type=int, nargs=6)
args = parser.parse_args()

print(args.enteros)
print(sum(args.enteros))
```
Ejecutar en la terminal
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo3.py 2 1 4 5 0 3 
```
El resultado es como muestra a continuación:

![Suma6](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1294/v1641313567/kipunaEC/argparse/ej3-min_o62fqs.png)
_Fig 5. Muestra 6 enteros que ingresan y su suma_

En el siguiente código especifico `nargs` como `nargs='*'`, puedo ingresar tantos valores como necesite. Imprimo los enteros que ingresen y sumo esos valores. 
```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('enteros', type=int, nargs='*')
args = parser.parse_args()

print(args.enteros)
print(sum(args.enteros))
```
Ejecutar en la terminal
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo3.py 7 4 9 10 2 0 1 5
```
En este ejemplo ingreso 8 valores, aparecerá la lista de los enteros ingresados y la suma de los mismos. Cuando no ingreso ningun valor como argumento, la lista aparece vacía.

![ej034](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1297/v1641317690/kipunaEC/argparse/ej034-min_gkzadw.png)
_Fig 6. Muestra una lista con los enteros ingresados y su suma (ejemplo usando nargs='*')_

En el siguiente código especifico `nargs` como `nargs='+'`, puedo ingresar tantos valores como necesite igual que con `nargs='*'`. La diferencia es que cuando no ingresa ningun valor aparece un mensaje de error. `nargs='+'` requiere al menos 1 valor

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('enteros', type=int, nargs='+')
args = parser.parse_args()

print(args.enteros)
print(sum(args.enteros))
```
Ejecutar en la terminal
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo3.py 7 4 9 10 2 0 1 5
```
![ej033](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1294/v1641318090/kipunaEC/argparse/ej035-min_l5pmwp.png)
_Fig 7. Muestra una lista con los enteros ingresados y su suma (ejemplo usando nargs='+')_

En el siguiente código especifico `nargs` como`nargs='?'`, este recibirá un solo valor.

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('entero', type=int, nargs='?')
args = parser.parse_args()

print(args.entero)
print(type(args.entero))
```
Ejecutar en la terminal, cuando no se ingresa un valor mostrara lo siguiente:

![ej03](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1291/v1641316764/kipunaEC/argparse/ej032-min_a4pvie.png)
_Fig 8. Muestra un entero e imprime e tipo de dato (ejemplo usando nargs='?')_

***

## Ejemplo4 - argparse
En este ejemplo aplico argumentos opcionales. Los argumentos opcionales se especifican con doble guión `--` o guión simple `-` [^1]. 

```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--text")
args = parser.parse_args()
if args.text:
    print(args.text)
```

Ejecutar en la terminal:
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo4.py --text Hola_Milu
```

![ej04](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_701/v1641491783/kipunaEC/argparse/ejemplo04_ofhp1y.png)
_Fig 9. Muestra el texto con un argumento opcional)_

En este ejemplo , si al ejecutar omito el argumento, no mostrará ningun mensaje porque se trata de un argumento opcional, así:

![ej041](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1297/v1641491999/kipunaEC/argparse/ejemplo041-min_yepdlr.png)
_Fig 10. Omito el argumento opcional y no aparece error)_

***

## Ejemplo5 - argparse
Este ejemplo será similar al ejemplo2, con la diferencia que ingreso dos argumentos uno posicional `nombre` y un argumento opcional `valor`. el programa imprimirá tu nombre y encontrará el cuadrado del número que ingrese.

```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("nombre", type=str, help = 'Ingresa tu nombre')
parser.add_argument("--valor", type=float, help = 'Ingresa un numero para elevar al cuadrado')
args = parser.parse_args()

print('Hola,',args.nombre)
if args.valor:
    print('El valor al cuadrado de', args.valor, 'es', args.valor**2)
```
Ejecuto en la terminal y obtengo:
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo5.py Milu
```
![ej051](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1292/v1641494546/kipunaEC/argparse/ejemplo051-min_awqdm6.png)
_Fig 11. Omito el argumento opcional y no aparece error_

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo5.py Milu --valor 5
```

![ej052](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1297/v1641494546/kipunaEC/argparse/ejemplo052-min_lbz1lv.png)
_Fig 12. Ejecutar script con el argumento posicional y el opcional_

***

## Ejemplo6 - argparse
En este ejemplo describo como funciona el parámetro [action](https://docs.python.org/es/dev/library/argparse.html#action) de `add_argument()`. Algunas acciones de `action` son: `'store'`, `'store_const'`, `'store_true'`, `'store_false'`, `'append'`, `'append_const'`, `'count'`

### `action='store'`
Es la opción por defecto y almacena el valor del argumento, por ejemplo:
```python
import argparse
import numpy as np

parser = argparse.ArgumentParser()
parser.add_argument('--nombre', action='store')
args = parser.parse_args()

print(args.nombre)
```
Ejecutar script
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo5.py --nombre Milu
```

![ej06](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1298/v1641586875/kipunaEC/argparse/ejemplo06-min_ffyivj.png)
_Fig 13. Argumento opcional; action='store'_


### `action='store_const'`
El valor del argumento es lo que se establece en la la palabra clave `const`
```python
import argparse
import numpy as np

parser = argparse.ArgumentParser()
parser.add_argument('--nombre', action='store_const', const= "Milu")
args = parser.parse_args()

print(args.nombre)
```
Para ejecutar este acript se debe ingresar `--nombre` sin nada más adicional porque `action='store_const'` guarda el valor establecido en `const` como variable, en este ejemplo se almacenará la palabra `"Milu"` . 

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo6.py --nombre
```
![ej061](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1295/v1642441463/kipunaEC/argparse/ejemplo061-min_l0ap3b.png)
_Fig 14. Argumento opcional; action='store_const'_

*Nota:* El script tiene la funcion `print` por lo que si se omite el nombre del argumento opcional `--nombre` por defecto imprimirá `none`

### `action='store_true'` y `action='store_false'`
Son casos especiales de `'store_const'` usados para almacenar los valores True y False respectivamente.

```python
import argparse
import numpy as np

parser = argparse.ArgumentParser()
parser.add_argument('--dato1', action='store_true')
parser.add_argument('--dato2', action='store_false')

args = parser.parse_args()
print(args.dato1)
print(args.dato2)
```
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo6.py --dato1 --dato2
```
![ej062](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1295/v1642445277/kipunaEC/argparse/ejemplo062-min_mdjlwn.png)
_Fig 15. Argumento opcional; action='store_true' y action='store_false'_

Si omito el argumento `--dato1` en la terminal, al ejecutar el script se crea automáticamente un valor predeterminado de `False` , y del mismo modo `store_false` establece de forma predeterminada `True` cuando el argumento de la línea de comandos no esté presente.

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo6.py 
```
Aunque no ingrese ningun argumento desde la terminal se imprimirá `True` o `False` porque en el scrip uso la funcion `print` para mostrar el estado de las variables, en este ejemplo muestra los valores por defecto. 

*Nótese la diferencia entre Fig 14 y Fig 15* 

![ej0622](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1297/v1642445434/kipunaEC/argparse/ejemplo0622-min_svnplc.png)
_Fig 16. Argumento opcional_

### `action='append'`
Añade a una lista cada valor ingresado como argumento
```python
import argparse
import numpy as np

parser = argparse.ArgumentParser()
parser.add_argument('-n','--numeros', action='append', type=float)
args = parser.parse_args()

print(args.numeros)
print(type(args.numeros))
```

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo6.py -n 1 -n 2 -n 3 -n 4 
```
![ej0624](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1296/v1642452031/kipunaEC/argparse/ejemplo064-min_bvacq8.png)
_Fig 17. action='append'_


### `action='append_const'` 
Almacena el valor de `const` en una lista, de acuerdo a los argumentos que ingresan desde la terminal.

El siguiente script almacena los valores de la densidad de varios líquidos, y desde la terminal se elige la densidad del elemento que desee.
```python
import argparse
import numpy as np

#Densidad [kg/m3] de algunos liquidos en una lista
parser = argparse.ArgumentParser()
parser.add_argument('--agua', dest='densidades', action='append_const', const= 1)
parser.add_argument('--aceite', dest='densidades', action='append_const', const=0.9)
parser.add_argument('--gasolina', dest='densidades',action='append_const',const=0.7)
parser.add_argument('--petroleo' , dest='densidades',action='append_const',const=0.8)

args = parser.parse_args()

print(args.densidades)
```
Escribo cuatro elementos para conocer sus desidades.
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo6.py --agua --aceite --gasolina --petroleo
```
![ej065](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1297/v1642457300/kipunaEC/argparse/ejemplo065-min_pn0tws.png)
_Fig 18. action='append_const'_

Escribo dos elementos para conocer sus densidades

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo6.py --agua --petroleo
```
![ej066](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1296/v1642457565/kipunaEC/argparse/ejemplo066-min_jpw3mc.png)
_Fig 19. action='append_const'_


### `action='extend'`
Extiende cada valor del argumento a una lista.

```python
import argparse
import numpy as np

#Densidad [kg/m3] de algunos liquidos en una lista
parser = argparse.ArgumentParser()
parser.add_argument("--foo", action="extend", nargs="+", type=int)

args = parser.parse_args()
print(args.foo)
```

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo6.py --foo 4213756 --foo 4
```
![ej067](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1297/v1642461137/kipunaEC/argparse/ejemplo067-min_bkm5ct.png)
_Fig 20. action='extend'_

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo6.py --foo 421 3 756 --foo 4
```
![ej068](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1297/v1642461379/kipunaEC/argparse/ejemplo068-min_juke58.png)
_Fig 21. action='extend'_

***

## Ejemplo7- argparse
En la [documentación oficial](https://docs.python.org/es/dev/library/argparse.html#module-argparse) de python encuentras [este ejemplo](https://docs.python.org/es/dev/library/argparse.html#example) que lo guardaré como `ejemplo7.py`, aquí explicaré como funciona. 
El código es el siguiente:
```python
import argparse

parser = argparse.ArgumentParser(description='Process some integers.')
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                    help='an integer for the accumulator')
parser.add_argument('--sum', dest='accumulate', action='store_const',
                    const=sum, default=max,
                    help='sum the integers (default: find the max)')

args = parser.parse_args()
print(args.accumulate(args.integers))
```
Primero revisemos la ayuda que muestra este script al momento de ejecutar.

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo7.py -h
```
![ej07](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1298/v1642698392/kipunaEC/argparse/ejemplo7-min_nm1lve.png)
_Fig 22. Mensajes de ayuda del ejemplo7_

* `usage`: Muestra la sintaxis que debe ingresar. Los comandos opcionales `[-h] [--sum]` y los argumentos posicionales `N [N ...]`, aparece los valores de **N** porque se especifica así en el parámetro `metavar`.
* `Process some integers.` es la leyenda que se agrega en la descripción.
* `positional arguments:` **N** representa números enteros que pueden ingresar al programa
* `optional arguments:` **-h** mensaje de ayuda. **--sum** suma los valores ingresados como **N**, por defecto obtiene el máximo valor de los enteros ingresados. 

Ahora ejecuto el programa sin el parámetro opcional 
```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo7.py 45 3 -23 4 -6 0
```
![ej071](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1292/v1642699211/kipunaEC/argparse/ejmplo7max-min_xfiwb9.png)
_Fig 23. Por defecto el ejemplo7 obtiene el máximo de los enteros ingresados_

Y ahora ejecuto el programa con el parámetro opcional `--sum`

```terminal
kipuna@kipuna-Satellite-L635:~/Escritorio$ python3 ejemplo7.py --sum 45 3 -23 4 -6 0
```
![ej072](https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_1297/v1642700497/kipunaEC/argparse/ejemplo7suma-min_dmzw4g.png)
_Fig 23. Con --sum el ejemplo7 suma los enteros ingresados_



[Gif]: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_728/v1633444807/kipunaEC/gifs/patricio5_h2janv.gif
[suscribirse]: https://www.youtube.com/channel/UCLHyReaGzfUcaiGoEN5jXEA "Clic para suscribirse en youtube"
[![Suscribirse][Gif]][suscribirse]

***
***
[comment]: ## video

[comment]: <div class="embed-container">

[comment]: <iframe width="586" height="342" src="https://www.youtube.com/embed/fiilnEu1_vM" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
[comment]: </iframe>

[comment]: </div>
[comment]: </div>

[comment]:  *** 

> Aprendan siempre, aprendan mucho — Mimi

***


## Referencias

[^1]: Python argparse documentación. *Guión simple - guión doble*. [https://docs.python.org/3/library/argparse.html#required](https://docs.python.org/3/library/argparse.html#required)
