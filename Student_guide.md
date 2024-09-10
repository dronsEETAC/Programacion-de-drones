# Programación de drones

## **1. Presentación**
En este taller vas a aprender a desarrollar programas en Python para **controlar la operación de
un dron**. Aprenderás a crear un programa con una **interfaz gráfica** que use botones para
ordenar al dron que despegue o vuele en una dirección determinada. El programa también presentará al
usuario un **mapa** en el que mostrará la posición del dron en todo momento y permitirá
**guiar el dron con las poses de tu cuerpo**, utilizando técnicas de reconocimiento de imagen.     
      
<img src="https://github.com/dronsEETAC/tallerTelecoRenta/assets/100842082/600f03c9-1c70-4ec0-a52f-87f934c3862c" width="400" height="200">


En este repositorio encontrarás:     
      
1. Los **códigos** de referencia para la realización del taller.
2. Material **escrito**.
3. **Vídeos** que te guiarán durante el proceso.     
     
Aprenderás instalando esos códigos, analizándolos, modificándolos y ampliándolos.     
    
El taller admite diferentes grados de implicación. Puedes limitarte a instalar los códigos, 
comprobar que funcionan correctamente y examinarlos. Eso no te llevará más de 1 hora.
Puedes también enfrentarte a unos cuantos retos concretos que te iremos proponiendo, y que
requerirán que añadas código de tu propia cosecha. **En el repositorio encontrarás los códigos
que resuelven esos retos**, para el caso en que necesites ayuda. Esta modalidad te llevará unas
2 horas. Finalmente, puedes abordar tus propios retos, porque seguro que te vas a imaginar
cosas. Ya no podemos indicarte cuántas horas te llevará eso, porque podrías consagrar tu vida
entera a añadir funcionalidades interesantes.
      
Los códigos que vas a desarrollar interactúan en realidad con un **simulador del dron**, de
manera que solo necesitas tu portátil, las instalaciones que te indicaremos y los códigos de
referencia. No obstante, tus códigos pueden hacer volar un **dron real**, para lo
cual tendrás que modificar solo un par de líneas de tu código.

      
<img src="https://github.com/dronsEETAC/tallerTelecoRenta/assets/100842082/60132ceb-70f2-4bd3-97b3-0b305ae12075" width="700" height="200">
     
Mira este vídeo para ver una demo de la aplicación que se desarrolla en este taller.

[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DryezfzIUBrE)](https://www.youtube.com/watch?v=ryezfzIUBrE)

## 2. Etapas del taller

El taller está organizado en 4 etapas, que se describen a continuación:

- **Etapa 1**: Se desarrolla un programa en **Python** con una **interfaz gráfica** basada en botones con
los que controlar la operación del dron (operaciones básicas como **armar, despegar, volar en
diferentes direcciones** o **aterrizar**). En esta etapa se plantean un par de **retos**, cuya solución
también puede encontrarse en el repositorio.

- **Etapa 2.A:** Se añade al resultado de la Etapa 1 un **mapa** que permite mostrar al usuario la
posición del dron en cada momento. También se plantean un par de **retos** que permiten al
usuario interactuar con el dron a través del mapa.

- **Etapa 2.B:** Se añade al resultado de la Etapa 1 el código necesario para guiar el dron mediante
las **poses del cuerpo**, detectadas a través de la cámara del portátil. De nuevo se plantearán dos
**retos** para ampliar las funcionalidades de esta versión.

- **Etapa 3:** Consiste en integrar en una única aplicación los desarrollos de las etapas anteriores,
puesto que las etapas **2.A** y **2.B** se desarrollarán **de manera independiente y en cualquier
orden.**

En este repositorio encontrarás un apartado dedicado a cada una de estas etapas en las que se
describirá (**con texto y videos**) las funcionalidades de la versión inicial de esa etapa, los retos
que te proponemos (y que también encontrarás resueltos) y una lista de posibles retos más
ambiciosos que esperamos que despierten tu interés.

## 3. Herramientas 

Para realizar el taller necesitarás instalar en tu ordenador las herramientas siguientes:

- **Git:** Es una herramienta muy popular para la gestión de versiones de código. Con esta herramienta
podrás instalar en tu ordenador (clonar) este repositorio y acceder a los códigos de las
diferentes etapas.<br />
https://git-scm.com/downloads

- **Mission Planner:** Es una aplicación de escritorio que **permite interactuar con el dron**. Por
ejemplo, permite configurar muchos parámetros del dron y darle ordenes típicas (armar,
despegar, volar a un punto dado, etc.). Mission Planner permite también poner en marcha un
**simulador del dron**, que llamaremos **SITL** (Software In The Loop). Tanto Mission Planner como
las aplicaciones que se desarrollan en este taller **interactúan con el simulador, exactamente
igual que como lo harían con el dron real**. Esto es ideal para desarrollar y verificar el correcto
funcionamiento de los códigos antes de usarlos para controlar el dron real (cosa que podrás
hacer si realizas el segundo taller al que hemos hecho referencia en la presentación).<br />
https://ardupilot.org/planner/docs/mission-planner-installation.html

- **Python:** Necesitarás un intérprete de Python. Puedes utilizar las versiones más actuales.<br />
https://www.python.org/downloads/

- **PyCharm:** Se trata de la aplicación más popular para el desarrollo de código en Python.
Asegúrate de instalar la versión denominada Community Edition, que es gratuita y más que
suficiente.<br />
https://www.jetbrains.com/pycharm/
     
Además, durante el taller tendrás que instalar en el entorno de desarrollo creado por Pycharm tres
librerías diferentes: pymavlink (necesaria para la comunicación con el dron), tkintermapview (para trabajar con mapas) y mediapipe (para procesar las imágenes tomadas por la cámara y detectar, por ejemplo, poses del cuerpo).


## 4. Estructura del repositorio

Una vez hayas instalado Git en tu ordenador, ya puedes clonar el repositorio, que está
organizado tal y como muestra en la figura:


<img src="https://github.com/dronsEETAC/tallerTelecoRenta/assets/100842082/b0cd63c6-6d10-44c2-8e68-70c6462b2edc" width="400" height="200">


En el repositorio puedes acceder al código de las 4 etapas, puesto que las diferentes versiones
de la aplicación están convenientemente etiquetadas. Por ejemplo, en la etiqueta **V1.1
tenemos el código base de la Etapa 1**, perfectamente operativo, en el que puedes aprender
cómo implementar una interfaz gráfica con botones para controlar el dron. En la etiqueta **V1.2
tienes el código después de haber resuelto los dos retos** que se te plantearán en esa etapa. De
la misma manera, encontrarás en la etiqueta **V2.A.1 el código base de la etapa 2.A** y en **V2.A.2
el código resultante de resolver los retos propuestos**.


## 5. Git

La herramienta **Git te permite crear ramas para tus propios desarrollos.** De hecho, la figura del apartado anterior
muestra que el código tiene una rama principal **(main)** que se **divide en dos ramas (mapa y
pose)** que luego **se funden de nuevo en la rama main.** **Tú puedes crear las ramas necesarias
para tus desarrollos.** Por ejemplo, la figura indica que se ha creado una rama llamada _reto1_ en
la que el usuario desarrollará el código para abordar los retos de la etapa 1. De la misma forma se
han creado las ramas reto2.A y reto2.B para los retos de esas etapas. Naturalmente, **con Git puedes moverte por esa estructura de ramas y versiones**, lo cual permite, por ejemplo, consultar el código del reto resuelto en caso de ser necesario.

En los dos vídeos siguientes puedes ver cómo **clonar el repositorio**, **moverte por las diferentes
versiones**, **crear las ramas** necesarias para tus propios desarrollos y **moverte por el repositorio
de una rama a otra** o de una versión a otra. En la descripción de los vídeos encontrarás un resumen de los **comandos de git** que se han usado en ambos vídeos.

[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DBST5Dj4PqZ4)](https://www.youtube.com/watch?v=BST5Dj4PqZ4)


[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DgvXLxkuPaog/1.jpg)](https://www.youtube.com/watch?v=gvXLxkuPaog/1.jpg)



## 6. Para empezar a programar

Una vez instalado **Git, Mission Planner, el intérprete de **Python** y Pycharm**, mira estos videos e
intenta reproducir en tu ordenador lo que ves en ellos.       
          
Los vídeos te muestran cómo **poner en marcha Mission Planner y el simulador SITL**. También muestran cómo hacer un programa sencillo que **envía comandos al simulador del dron**, usando la librería _**DronLib**_, que está incluida en el repositorio de este taller.


[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DUPyklN9namM)](https://www.youtube.com/watch?v=UPyklN9namM)

[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DP_NCKA_3-PQ)](https://www.youtube.com/watch?v=P_NCKA_3-PQ)

## 7. La librería DronLib

DronLib es la librería que vamos a usar para **darle ordenes al dron** (tanto al simulador SITL
como al dron real). Es una **librería en desarrollo** (y por tanto, no exenta de fallos) que
pretende ser una alternativa a DroneKit, que es la más utilizada, pero que ya no está en
mantenimiento y tiene problemas de compatibilidad con las versiones más avanzadas del intérprete de Python. No obstante, si quieres experimentar con DroneKit aquí puedes ver una solución al problema de compatibilidad detectado.

<img src="https://github.com/dronsEETAC/Taller-de-Drones-TelecoRenta/assets/100842082/841e7a62-ef19-4841-be70-e6079cf7e9c4" width="400" height="200">


La librería esta implementada en forma de clase **(la clase Dron)** con sus atributos y una
variedad de métodos para operar con el dron. La clase con los atributos está definida en el
fichero _Dron.py_ y los métodos están en los diferentes ficheros de la carpeta _modules_
(connect.py, arm.py, etc.).

Muchos de los métodos pueden activarse **de forma bloqueante o de forma no bloqueante**. En
el primer caso, **el control no se devuelve al programa que hace la llamada hasta que la
operación ordenada haya acabado**. Si la llamada es no bloqueante entonces **el control se
devuelve inmediatamente** para que el programa pueda hacer otras cosas mientras se realiza la
operación.

Un buen ejemplo de método con estas dos opciones es _takeOff_, que tiene la siguiente cabecera:

```
def takeOff(self, aTargetAltitude, blocking=True, callback=None , params = None)
```

Al llamar a este método hay que pasarle como parámetro la **altura de despegue**. Por defecto la
operación es **bloqueante**. Por tanto, el programa que hace la llamada no se reanuda hasta que 
el dron esté a la altura indicada. En el caso de usar la opción no bloqueante se puede indicar el
nombre de la función que queremos que se ejecute cuando la operación haya acabado (que
llamamos habitualmente **callback**). En el caso de  takeOff, cuando el dron  esté a la altura indicada
se activará la funcion callback. Incluso podemos indicar los parámetros que queremos que
se le pasen a ese callback  en el momento en que se active. **Recuerda que self no es ningún parámetro**. 
Simplemente **indica que este es un método de una clase** (en este caso, la clase Dron).

Los siguientes ejemplos aclararán estas cuestiones.

_Ejemplo 1_

```
from Dron import Dron
dron = Dron()
dron.connect ('tcp:127.0.0.1:5763', 115200) # me conecto al simulador
print (‘Conectado’)
dron.arm()
print (‘Armado’)
dron.takeOff (8)
print (‘En el aire a 8 metros de altura’)
```

En este ejemplo todas las llamadas son bloqueantes.


_Ejemplo 2_

```
from Dron import Dron
dron = Dron()
dron.connect ('tcp:127.0.0.1:5763', 115200) # me conecto al simulador
print (‘Conectado’)
dron.arm()
print (‘Armado’)
dron.takeOff (8, blocking = False) # llamada no bloqueante, sin callback
print (‘Hago otras cosas mientras se realiza el despegue’)
```
En este caso la llamada no es bloqueante. El programa continua su ejecución 
mientras el dron  realiza el despegue. 

_Ejemplo 3_

```
from Dron import Dron
dron = Dron()
dron.connect ('tcp:127.0.0.1:5763', 115200) # me conecto al simulador
print (‘Conectado’)
dron.arm()
print (‘Armado’)    
     
def enAire (): # esta es la función que se activa al acabar la operación (callback)
    print (‘Por fin ya estás en el aire a 8 metros de altura’)
      
# llamada no bloqueante con callback
dron.takeOff (8, blocking = False, callback= enAire)
print (‘Hago otras cosas mientras se realiza el despegue’)
```
De nuevo una llamada no bloqueante. Pero en este caso le estamos indicando que cuando 
el dron esté a la altura indicada ejecute la función enAire, que en este caso simplemente
nos informa del evento.     
       
_Ejemplo 4_

```
from Dron import Dron
dron = Dron()
dron.connect ('tcp:127.0.0.1:5763', 115200) # me conecto al simulador
print (‘Conectado’)
dron.arm()
print (‘Armado’)

def informar (param):
   print (‘Mensaje del dron: ‘, param)

# Llamada no bloqueante, con callback y parámetro para el callback
dron.takeOff (8, blocking = False, callback= informar, params= ‘En el aire a 8 metros de altura’)
print (‘Hago otras cosas mientras se realiza el despegue. Ya me avisarán’)
```
En este caso en la llamada no bloqueante añadimos un parámetro que se le pasará al callback en 
en el momento de activarlo. De esta forma, la misma función informar se puede usar  como callback
para otras llamadas no bloqueantes. Por ejemplo, podríamos llamar de forma no bloqueante al método 
para aterrizar y pasar le como callback también la función informar, pero ahora con elm  parámetro
'Ya estoy en tierra', que es lo que escribiría en consola la función  informar en el momento del aterrizaje.

_Ejemplo 5_

```
from Dron import Dron
dron = Dron()
# conexión con identificador del dron
dron.connect ('tcp:127.0.0.1:5763', 115200, id=1)
print (‘Conectado’)
dron.arm()
print (‘Armado’)
     
# La función del callback recibirá el id del dron como primer parámetro
def informar (id, param):
    print (‘Mensaje del dron ‘+str(id) + ‘: ‘ + param)
    
dron.takeOff (8, blocking = False, callback= informar,
params= ‘En el aire a 8 metros de altura’)
print (‘Hago otras cosas mientras se realiza el despegue. Ya me avisarán’)
```

En este ejemplo usamos la opción de identificar al dron **en el momento de la conexión**
(podríamos tener varios drones, cada uno con su identificador). Si usamos esa opción entonces
el método de la librería va a añadir siempre ese identificador como primer parámetro del
callback que le indiquemos.

La modalidad no bloqueante en las llamadas a la librería es especialmente útil **cuando
queremos interactuar con el dron mediante una interfaz gráfica**. Por ejemplo, no vamos a
querer que se bloquee la interfaz mientras el dron despega. Seguramente querremos seguir
procesando los datos de telemetría mientras el dron despega, para mostrar al usuario, por
ejemplo, la altura del dron en todo momento.

### Métodos de la clase Dron
En la tabla que se indica se describen los métodos de la clase Dron que se usan en este taller. En
muchas de ellas aparecen los tres parámetros requeridos para implementar la modalidad no
bloqueante (_blocking_, _callback_ y _params_).    
     
[Métodos de la clase Dron](tabla_dronLib.pdf)   

## 8. Etapa 1: Interfaz con botones

### Versión inicial

Accede al código de la versión inicial de esta etapa, que tiene la etiqueta **“v1.1”**. Al ejecutar el
código del programa principal (_Dashboard.py_) se mostrará una sencilla interfaz gráfica con
botones para realizar las **operaciones más básicas con el dron: conectar, armar, despegar,
mover el dron en diferentes direcciones y retornar a casa.**

Fíjate en el código que crea la interfaz gráfica basada en botones, que utiliza la **librería tkinter**.
Parece algo complejo, pero no lo es. Simplemente hay que imaginarse la interfaz como **una
matriz de filas y columnas**. El código indica qué elemento gráfico hay que colocar en cada
fila/columna de esa matriz. La mayoría de esos elementos son **botones**, pero algunos son
**_frames_** que internamente también están organizados como pequeñas matrices con sus filas,
sus columnas y sus elementos. Fíjate que hay algunos elementos de la interfaz que no se usan
y que puedes aprovechar si decides abordar los retos que te proponemos más adelante.

También es importante que veas cómo se usa nuestra librería con las funciones para controlar
el dron. Fíjate especialmente en el uso de las **llamadas no bloqueantes** y la forma en que se
indica qué función hay que ejecutar cuando haya acabado la operación solicitada.

Este vídeo contiene una **explicación del código de esta versión** y una **demostración de la
aplicación en funcionamiento**. Fíjate que para ejecutar el código tendrás que instalar la librería
**_pymavlink_**.


[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DRza4vbXaFp0)](https://www.youtube.com/watch?v=Rza4vbXaFp0)


### Retos

Te proponemos dos retos sencillos, cuya solución encontrarás en el código etiquetado con
“**v1.2**”.

- **Reto 1**: Añade botón para hacer que el dron aterrice en el punto sobre el que se encuentra.
Échale un vistazo a la librería **dronLib**. Seguro que encuentras allí la función que necesitas.

- **Reto 2**: Añade algún elemento a la interfaz que te permita introducir la altura a la que quieres
que despegue el dron (que en la versión inicial es una altura fija).

### Más retos

Aquí tienes una lista con otros retos que podrías plantearte, si tienes ganas y tiempo.
Naturalmente **tendrás que investigar un poco las librerías dronLib y pymavlink** para ver qué cosas se
pueden hacer con el dron:

1. Introduce un elemento de tipo _Scale_ (como el que se usa para especificar la velocidad
de vuelo) para especificar la altura de despegue.

3. Introduce los elementos necesarios para hacer que el **dron rote un cierto ángulo**
cuando está en el aire (cambio de heading).

5. Introduce algún elemento para que se muestre en todo momento **la altura** que tiene el
dron.


## 9. Etapa 2.A: Interfaz con mapa

### Versión inicial

Puede encontrarse en el tag “**v2.A.1**”. La novedad más importante es la aparición de un **botón
que abre una ventana nueva**, cuyo código está en el fichero _MapFrame.py_, en el que se
muestra un **mapa navegable**, igual que los que nos muestra Google Maps o el propio Mission
Planner. En ese mapa podemos hacer que **se muestre el dron en el mapa** y **seguir sus movimientos según
le indiquemos con los botones de navegación**, exactamente igual que los podemos seguir en el
mapa de Mission Planner. Analizando el código de esta versión aprenderás a **mostrar un mapa
de la zona que quieras** (indicando las coordenadas geográficas, a colocar una imagen en el 
mapa (por ejemplo, el icono del dron), a **capturar los eventos de ratón sobre el mapa** y **fijar
marcas o dibujar líneas en el mapa**.

La función más interesante de esta versión es la **creación de un geofence**: un
**polígono que encierra al dron**, de manera que el dron no pueda escapar del interior de ese
polígono. Como puedes imaginar, esa es una **medida de seguridad extremadamente útil** para
realizar vuelos reales. Observa cómo se fijan los puntos (coordenadas geográficas) que definen
el polígono y còmo se prepara la información que hay que enviarle a la librería de control del
dron para que establezca el geofence. Finalmente, es necesario **activar el geofence e indicar
qué acción debe hacer el dron si llega al límite del greofence**, que es nuestra aplicación será
quedarse parado en ese límite (fíjate ya de paso en la manera de cambiar cualquiera de los
muchos parámetros que tiene el dron, y que puedes listar desde Mission Planner clicando en
Config -> _Full parameter list_).

Este vídeo contiene una explicación del código de esta versión y una demostración de la
aplicación en funcionamiento. Fíjate que para ejecutar el código tendrás que instalar la librería
[**tkintermapview**](#installs).


[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DbQNr8IJ5veA)](https://www.youtube.com/watch?v=bQNr8IJ5veA)


### Retos

Los retos que te proponemos ahora no van a ser tan sencillo como los de la versión anterior.
Los encontrarás resueltos en la versión etiquetada con “**V.2.A.2**”.

- **Reto 1**: Introduce los elementos necesarios para poder **marcar un punto en el mapa** y hacer
**que el dron vuele hasta ese punto**. Para implementar esta funcionalidad necesitarás la función
_goto_ de la librería.

- **Reto 2**: Introduce los elementos necesarios para que **al clicar un botón se dibuje en el mapa el
rastro que deja el dron en su movimiento**. Ese botón debe servir para **activar** el rastro y para
**borrarlo**.

### Más retos

La lista de cosas que se pueden hacer es esta versión es infinita. Te proponemos algunos retos
(en muchos casos tendrás que investigar qué parámetros del dron hay que modificar):

1. Investiga cómo hacer para que la acción que realice el dron al **llegar al límite del
geofence sea un RTL** (retornar a casa)

2. El geofence no sólo tiene perímetro. También tiene **altura**. Si haces despegar el dron a
una altura superior a la que tiene el geofence se producirá un error y no despegará.
Introduce los elementos necesarios para poder **definir la altura que debe tener el
geofence**.

3. Cambia lo necesario para ver volar el dron sobre el césped del **Nou Camp**.

4. Introduce un botón que permita **activar o desactivar el geofence**, según convenga.

5. Modifica la función de dibujar el rastro para que puedas **activar o desactivar** **(no
borrar**) el dibujo del rastro. De esta manera podrás hacer dibujos sobre el área de
vuelo (como un pictionary que podrían ver los extraterrestres).


## 10. Etapa 2.B: Control del dron mediante poses

Puede encontrarse etiquetada con “**v2.B.1**”. Esta etapa puede realizarse inmediatamente
después de la etapa 1 (**no se necesita el código desarrollado en la etapa 2.A**).

En la versión inicial se ha incluido un botón que abre una ventana en la que se muestran
**diferentes poses del cuerpo** de manera que si el usuario hace alguna de esas poses delante de
la cámara de su portátil el dron realizará la operación asociada a la pose (por ejemplo, volar
hacia el norte). **En la versión inicial hay tres poses implementadas y el reto es implementar
otras tres**.

Para implementar esta funcionalidad se ha usado la librería [_mediapipe_](#installs) (**que hay que instalar**).
Esta librería tiene una función a la que **se le pasa la imagen de un cuerpo e identifica en ese
cuerpo un total de 32 puntos clave** (landmarks). La función nos devuelve una lista con las
coordenadas de cada uno de esos puntos clave, asumiendo que la imagen es un espacio de **2D
en el que la coordenada x (eje horizontal) va de 0 a 1 y la coordenada y (eje vertical) va de 0 a
1**. De esta forma, la **esquina superior izquierda** tiene la coordenada **(0,0)** y la **inferior derecha**
tiene la coordenada **(1,1)**.

<img src="https://github.com/dronsEETAC/tallerTelecoRenta/assets/100842082/9a4d7fba-22fa-44f6-a9ce-591faa6b324e" width="400" height="400">

A partir de esta lista de coordenadas es fácil determinar si la pose del cuerpo es una
determinada, comprobando la posición relativa de cada punto de la pose con el resto. En las
poses implementadas solo se usan los puntos clave **del 11 al 16**.

Observa que en el código tenemos la clase _BodyFrame_ que muestra las imágenes guía y tiene
los botones para poner en marcha la funcionalidad. En esa clase, una vez se obtiene una
imagen de la cámara se envía a la clase _PoseDetector_ en la que se hacen las comprobaciones
necesarias para determinar qué pose hay en la imagen. Al recoger el resultado, la clase
_BodyFrame_ da la orden correspondiente al dron.


[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3D2kP3vmNhnFM)](https://www.youtube.com/watch?v=2kP3vmNhnFM)



### Reto

Entre las imágenes de referencia que aparecen al poner en marcha la versión inicial **hay 3 en
rojo que no están implementadas**. Modifica el código para hacer que _PoseDetector_ detecte
esas 3 nuevas poses y modifica el código de _BodyFrame_ para **asociar a cada una de esas 3
poses una nueva operación del dron** (las que tu elijas)
    
### Más retos

El número de poses que impliquen exclusivamente los puntos clave del 11 al 16 es limitado.
Puedes inventar poses más complejas en las que intervengan muchos más puntos. **Por
ejemplo, trata de implementar tus poses de yoga favoritas**.

La librería _mediapipe_ incluye muchas otras funcionalidades que pueden inspirarte aplicaciones
interesantes. Por ejemplo, hay funciones para detectar puntos clave de las **manos** (¿puedes
hacer que el dron despegue si haces ante la cámara con la mano el signo de OK?). Otras
funciones detectan puntos clave de la cara (**¿puedes hacer que el dron aterrice si le guiñas el
ojo izquierdo?**).    

<img src="https://github.com/dronsEETAC/tallerTelecoRenta/assets/100842082/f73f9463-336e-4258-bb2d-431084ce1d10" width="400" height="200">

## 11. Etapa 3: Versión integrada
Puedes encontrar en el tag “**v3**” la versión final que integra todos los retos propuestos en las etapas anteriores. 
     
### Reto
Naturalmente, tu reto en esta etapa es integrar todos tus desarrollos (los retos que te hemos propuesto en cada etapa y los que te hayas propuesto tu mismo) en una sola versión. En esa tarea tendrás que usar el comando git para hacer el merge, tal y como viste en los vídeos del apartado 5. Es muy probable que te surjan conflictos que tendrás que resolver tal y como se indicó en esos vídeos.

