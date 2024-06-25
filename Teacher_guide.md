# Guía del profesor
## 1. Presentación   
Este apartado está destinado a profesorado que quiera utilizar el material de este taller en su propia docencia. Aquí pueden encontrarse aclaraciones sobre puntos clave del taller, recomendaciones de cómo diseñar actividades para la propia asignatura y materiales adicionales para abordar retos cada vez más ambiciosos, como por ejemplo, aumentar las capacidades de la librería propuesta para controlar el dron, montar y configurar un dron real que pueda ser controlado por la aplicación desarrollada, o incorporar a la aplicación funcionalidades para el reconocimiento de objetos mediante redes neuronales.    

## 2. Observaciones sobre el taller  

## 3. ¿Cómo usar el material del taller en una asignatura?       
En este apartado se hacen sugerencias sobre cómo diseñar una actividad para una asignatura usando el material de este taller. Se proponen dos casos: una asignatura semipresencial y una on-line.      

### Asignatura semipresencial    
Asumiremos que la asignatura tiene sesiones de clase de 2 horas y que los alumnos deben dedicar 2 horas de trabajo personal entre sesiones de clase. La actividad que se propone se extiende a lo largo de 3 sesiones, pero puede amplicarse fácilmente, en función de la ambición del los grupos al plantearse nuevos retos. A continuación se describe el contenido de cada sesión y el trabajo que deben realizar los alumnos entre sesiones.   

| Plan  | 
| ------------- | 
| _Sesión 1_    | 
| Se presenta la actividad y se hace una demostración como la que se muestra en el vídeo del apartado 1 de la guía del estudiante. También se hacen las demostraciones y explicaciones contenidas en el apartado 6 de la guía. Se explica brevemente cómo está organizado el repositorio con el código (apartado 4). Finalmente se muestra algún ejemplo de cómo usar la librería DronLib, como los que hay en el apartado 7. | 
|  _Trabajo fuera del aula_ | 
| Los alumnos instalan las herramientas (sección 3 del repositorio), instalan el repositorio y estudian el contenido del apartado 5.  |    
| _Sesión 2_    | 
| Se forman grupos de 4 alumnos que comparten las dificultades que hayan podido tener en el trabajo fuera del aula. El docente realiza las aclaraciones necesarias y resuelve las dudas que se haya producido. Los alumnos realizan la ETAPA 1 con sus retos. La tarea es individual aun que con el apoyo en primera instancia de los compañeros de grupo y en segunda instancia del docente. Al final de la sesión los grupos se dividirán en dos subgrupos: el subgrupo mapa (que se enfrentará a la etapa 2.A con sus retos) y el subgrupo pose (que se enfrentará a la etapa 2.B con sus retos). | 
|  _Trabajo fuera del aula_| 
|Cada alumno desarrolla individualmente la etapa que le corresponde, posiblemente apoyándose en su compañero de subgrupo que trabaja la misma etapa.   |  
| _Sesión 3_    | 
| Los grupos se reunen. Primero los miembros de cada subgrupo ponen en común el trabajo y después explican a los compañeros del otros subgrupo en qué ha consistido su etapa. El docente realiza las aclaraciones necesarias y resuelve las dudas que se haya producido. Los grupos realizan la ETAPA 3 en la que se integran los desarrollos realizados hasta el momento. Los grupos eligen los retos que quieren abordar a partir de ese momento y organizan el trabajo a realizar.| 
|  _Trabajo fuera del aula_   | 
|Los alumnos trabajan en sus retos de acuerdo con el plan establecido. |  
| _Sesión 4_    | 
| En esta última sesión los grupos realizan una demo al docente y luego una evaluación cruzada, de esta manera sus compañeros pueden ver el trabajo realizado por otros grupo. |      

En el caso de que los retos que se planteen los grupos sean ambiciosos puede ser conveniente alargar el proceso intertando alguna sesión adicional antes de la sesión final, para supervisar el trabajo y resolver las dudas que se estén produciendo.

## 4. Ampliación de la librería dronLib
La librería que se ha usado en el taller (DronLib) está en desarrollo. En la versión disponible en el repositorio del taller tiene un mínimo conjunto de métodos, suficientes para los objetivos del taller. Pero naturalmente es posible ampliar en gran medida las funcionalidades de la librería. Este puede ser un proyecto interesante: organizar a los alumnos del curso en equipos y encargar a cada equipo que desarrolle algunas funcionalidades adicionales a la librería.    
      
No es un ejercicio fácil, porque hay que hacer una búsqueda de información sobre qué cosas pueden hacerse con la librería pymavlink que, aunque es fácil encontrar información sobre ella en internet, no es una librería fácil de usar. Por otra parte, hay que implementar después los nuevos métodos siguiendo la filosofía de DronLib (por ejemplo, implementando la versión bloqueante y la no bloqueante, cuando eso tenga sentido.     
     
Veamos un ejemplo que ilustra cómo habría que afrontar este reto. Supongamos que queremos añadir a la librería un método que nos permita leer los puntos del geofence, en el caso de que haya alguno cargado en el dron. Esto podría ayudarnos a mejorar las funcionalidades de la etapa 2A, añadiendo el código necesario para pintar en el mapa, después de la conexión con el dron, el geofence que ya esté cargado en el dron, si es que hay alguno.     
    
Esta funcionalidad requiere primero averiguar cuántos puntos tiene el geofence y luego leer uno a uno esos puntos para colocarlos en una lista y retornar esa lista al programa que llama a la función.     
     
El número de puntos del geofence es uno de los parámetros del dron: ‘FENCE_TOTAL’. En el taller ya se ha explicado cómo leer cualquiera de los parámetros. Por otra parte, después de un cierto esfuerzo de búsqueda para averiguar cómo pedir al dron los puntos del geofence veremos que eso puede hacerse enviando un mensaje de tipo _MAVLink_fence_fetch_point_message_, en el que, entre otros parámetros, se le indica el número de orden del punto que quiere leerse. Podemos ya imaginar un bucle en el que damos tantas vueltas como nos indique el valor del parámetro ‘FENCE_TOTAL’, de manera que en cada iteración recuperamos uno de los puntos del geofence y lo añadimos a la lista.
Naturalmente, tiene sentido implementar una versión bloqueante y una no bloqueante de este método, porque la operación no será instantánea y no querremos dejar bloqueada la interfaz gráfica. De hecho, la implementación de este método debe parecerse mucho al método getParameters, porque también hay que pedir cosas al dron una a una y recopilarlas en una lista que debe proporcionar como resultado. Y también tiene la versión bloqueante y la no bloqueante.     
      
Con todo esto podemos ya escribir el código del nuevo método, que incorporaremos a la librería.   

```
def _getGEOFence(self, callback=None):
    #pido el número de puntos del geofence
    self.vehicle.mav.param_request_read_send(
        self.vehicle.target_system,self.vehicle.target_component,
        'FENCE_TOTAL'.encode(encoding="utf-8"),
        -1
    )
    message = self.vehicle.recv_match(type='PARAM_VALUE', blocking=True).to_dict()

    total = int(message["param_value"])
    print ('total ', total)
    if total == 0:
        # no hay fence
        fencePoints = None
    else:
        fencePoints = []
        idx = 0
        while idx < total:
            print ('vamos a por el ', idx)
            # solicito el punto siguiente
            message = dialect.MAVLink_fence_fetch_point_message(target_system=self.vehicle.target_system,
                                                                target_component=self.vehicle.target_component,
                                                                idx=idx)
            self.vehicle.mav.send(message)

            # espero que me llegue el punto solicitado
            message = self.vehicle.recv_match(type=dialect.MAVLink_fence_point_message.msgname,
                                        blocking=True)
            message = message.to_dict()
            latitude = message["lat"]
            longitude = message["lng"]
            fencePoints.append ({
                'lat': latitude,
                'lon': longitude
            })
            idx = idx + 1
    # elimino el primer punto y el último
    fencePoints = fencePoints[1:-1]
    if callback != None:
        if self.id == None:
            callback(fencePoints)
        else:
            callback(self.id, fencePoints)
    else:
        return fencePoints


def getGEOFence(self, blocking=True, callback=None):
    if blocking:
        return self._getGEOFence()
    else:
        getGEOFenceThread= threading.Thread(target=self._getGEOFence, args=[callback])
        getGEOFenceThread.start()
```
   
El código de este método hay que ubicarlo en alguno de los ficheros de la carpeta módulos. Lo correcto sería añadirlo al fichero _dron_setGeofence.py_, aunque tras esta incorporación quizá habría que cambiar el nombre a este fichero. Finalmente, hay que añadir los nombre de los nuevos métodos en el fichero _Dron.py_:    

```
from modules.dron_setGeofence import setGEOFence, _setGEOFence, getGEOFence, _getGEOFence
```
     
Naturalmente, el trabajo no puede dares por acabado sin haber hecho una prueba de que el nuevo método funciona correctamente, tanto en su versión bloqueante como en la no bloqueante. En el código de la etapa 2A sería fácil hacer una llamada inmediatamente después de haber creado el geofence, para comprobar que el nuevo método ha leído correctamente los puntos del geofence.

## 5. Reconocimiento de objetos mediante redes neuronales
Uno de los usos de los drones que más se están extendiendo es el reconocimiento de objetos desde el aire (por ejemplo, para contabilizar el número de personas en una manifestación o el número de ovejas en el rebaño). Las técnicas más utilizadas actualmente para este propósito son las redes neuronales convolucionales, cuyo desarrollo se ha visto favorecido por las mejoras de los algoritmos, el aumento de la capacidad de computación accesible para todos y el aumento de colecciones de imágenes necesarias para el entrenamiento de las redes.
Aprender cómo funcionan las redes neuronales para reconocer objetos e incorporar esa funcionalidad a la aplicación desarrollada en este taller puede ser una aventura apasionante.    
      
Este es un tutorial básico sobre cómo crear una red neuronal e integrarla en una aplicación en Python.   


[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DWwxhAen-rvc)](https://www.youtube.com/playlist?list=PLyAtSQhMsD4qWd33j4rxHd13iO_GUXK4N)    

Este es el repositorio con el código que se usa en el video: [![DroneEngineeringEcosystem Badge](https://img.shields.io/badge/TelecoRenta-codigo_tutorial_redes_neuronales-blue.svg)](https://github.com/dronsEETAC/TutorialRedesNeuronales.git)



## 6. Modelos de comunicación
La aplicación desarrollada en el taller utiliza un modo de comunicación que denominamos directo. El propio código de la interfaz de usuario es el que ejecuta las operaciones de control del dron, llamando a los métodos adecuados de la clase Dron, dependiendo, por ejemplo, del botón pulsado por el usuario. Naturalmente, el portátil en el que se ejecuta la aplicación tiene que estar conectado directamente al dron a través de la radio de telemetría.    

Una organización alternativa es lo que llamamos comunicación global. En este caso, existe un servicio especial, que solemos denominar autopilotService, que está separado de la interfaz gráfica y que es el responsable de controlar el dron. En este caso, cuando el usuario pulsa un botón la interfaz gráfica hace una petición al autopilotService que es el que finalmente da la orden al dron.
El modelo de comunicación global es el adecuado cuando el dron tiene capacidad de computación a bordo (por ejemplo, porque le hemos instalado una Raspberry Pi). En ese caso, el autopilotService se ejecutaría en la Raspberry Pi y la aplicación con la interfaz gráfica en el portátil. Ambos dispositivos estarían conectados a internet de manera que la aplicación enviaría sus peticiones (y recibiría resultados) a través de internet.     
    
También es el adecuado cuando queremos que sean varios usuarios los que puedan controlar el dron, cada uno desde su portátil, de manera que cualquier usuario podría enviar su petición al autopilotService, que podría estar ejecutándose en el portátil de cualquiera de ellos.    
     
Entre los diferentes modelos de comunicación a través de internet que pueden usarse, uno especialmente adecuado para este contexto es la comunicación a través de un bróker que implementa el protocolo MQTT. De acuerdo con este modelo, los dispositivos/procesos que quieren comunicarse (en este caso la aplicación y el autopilotService) lo hacen mediante un mecanismo de subscripción/publicación. Todos los implicados se conectan al bróker y cuando uno de ellos hace una publicación sobre un tema determinado (por ejemplo, un comando para el autopilotService) todos los subscritos a ese tema reciben del bróker una notificación. El protocolo MQTT es uno de los más usados en el mundo del internet de las cosas (IoT) porque es muy intuitivo y ligero.    
      
En estos vídeos puede encontrarse una explicación de todos estos conceptos, que se ilustran con un ejemplo.   


[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DcWMWHKHL0zc)](https://www.youtube.com/playlist?list=PLyAtSQhMsD4padff51h_2iO-8Mcwin_Y5)     

Y aquí puede encontrarse una explicación sencilla de como usar un bróker MQTT en Python.       
   
[MQTT Python](https://www.emqx.com/en/blog/how-to-use-mqtt-in-python) 

Se abre aquí una puerta al apasionante mundo de las comunicaciones a través de internet y a la posibilidad de plantear interesantes y divertidos proyectos. El más obvio de todos es construir un sencillo autopilotService y modificar la aplicación desarrollada en este taller para que trabaje en modo global, siguiendo el ejemplo que se muestra en el vídeo anterior. Y a partir de ahí es fácil imaginar retos divertidos como, por ejemplo, implementar un juego en el que diferentes usuarios cooperan para completar una misión, turnándose para llevar el dron de un sitio a otro. O incluso un juego de competición en el que cada usuario tiene que llevar el dron a un destino concreto y el sistema va asignando turnos de manera aleatoria para que cada usuario disponga de un periodo de tiempo (quizá también aleatorio) para acercar el dron a su objetivo antes de perder el turno.     
      
## 7. Web Apps
Para poder usar la aplicación que se ha desarrollado en este taller es necesario instalarla en el portátil que se va a conectar al dron. Imaginemos ahora que queremos controlar el dron desde nuestro teléfono móvil y que, además, no queremos tener que instalar ninguna aplicación en el teléfono (que lo tenemos a tope de apps). Ese interesante objetivo nos empuja al mundo de las web Apps.     
       
Una web app no es más que un servidor web que se está ejecutando en algún servidor conectado a internet. Desde el móvil podemos conectarnos a esa web exactamente igual que nos conectamos a cualquier otra (como, por ejemplo, un periódico digital). Pero ahora lo que nos va aparecer en la pantalla del móvil es un conjunto de botones para controlar el dron. Incluso lo que vemos en el móvil puede parecerse bastante que lo que muestra la interfaz gráfica de la aplicación desarrollada en este taller.     
     
La web app solo puede trabajar en modo de comunicación global (ver el apartado anterior), de manera que al pulsar un botón la web app hace una publicación en el bróker para que éste notifique la petición al autopilotService, que ejecutará la operación correspondiente con el dron.     
       
El mundo de las web apps no es fácil, pero es altamente motivador. Nos aleja de la programación en Python porque ahora hay que programar en JavaScript, TypeScript, HTML, CSS, etc. Aquí puede accederse a un tutorial que puede ayudar a introducirse en el tema, y que incluye aspectos tales como comunicaciones a través de un bróker MQTT.

[![](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DXCn9stPZ4iY)](https://www.youtube.com/playlist?list=PL64O0POFYjHoeq8dfP-XYPCoNlehSiR_B)     

El código que se desarrolla a lo largo de ese tutorial puede encontrarse aqui:      
[![DroneEngineeringEcosystem Badge](https://img.shields.io/badge/telecoRenta-codigo_tutorial_vue_-blue.svg)](https://github.com/dronsEETAC/TutorialVue.git)

## 8. El dron   
La aplicación que se desarrolla en este taller controla un dron simulado. Esto permite tener en un portátil todas las herramientas necesarias para desarrollar la actividad (incluido el simulador SITL). Como es natural, un paso más es hacer que la aplicación controle un dron real, para lo cual, en general, bastará modificar un par de líneas de código, precisamente las que especifican si la aplicación debe conectarse al simulador o al dron real.    

El dron recomendado es el que se muestra en las imágenes. Partiendo del kit que contiene todos los componentes, el dron puede montarse, configurarse y prepararse para el vuelo en unas 6 horas (dependiendo en parte de la habilidad manual de los implicados). Ese proceso es altamente formativo porque se toca temas relacionados con la electrónica, la mecánica, la física, la aerodinámica, etc.    

<img src="https://github.com/dronsEETAC/Taller-de-Drones-TelecoRenta/assets/100842082/abbcd66b-1b0a-45e3-91c6-09b227d9f2f4" width="500" alt="">

Aquí puede encontrarse una [guía](materiales_profesorado/guia_montaje.pdf),que indica cómo adquirir el kit (cuyo precio es de aproximadament 1500 euros) y describe paso a paso el proceso de montaje, configuración y preparación para el vuelo (y naturalmente también explica qué hay que cambiar en la aplicación para que actúe sobre el dron real).     
      
Es importante tener presente que el dron resultante no puede volarse en cualquier sitio. La normativa actual impone importantes restricciones al respecto. Por este motivo, recomendamos que antes de emprender la aventura de adquirir el kit, montar y configurar el dron se haga una valoración de las posibilidades existentes para volar el dron. Para ello, el contenido del último apartado de la guía (Dónde volar) puede ser de ayuda.

## 9. Raspberry Pi
En uno de los videos mencionados en el apartado 6 se sugiere un escenario interesante en el que el autopilotService se ejecuta en una Raspberry Pi, que naturalmente tiene que estar conectada a internet para recibir las notificaciones del bróker cuando nuestra aplicación solicite algún servicio.    
    
En una situación real, la Raspberry Pi estaría instalada en el dron y conectada al autopiloto sobre el que operaría directamente para realizar la operación solicitada desde la aplicación.     
    
Pero puede ser interesante hacer que la Raspberry Pi no actúe sobre el autopiloto real sino sobre el simulador. Esto puede ser útil para verificar que el código funciona correctamente antes de instalar la Raspberry Pi en el dron y hacer pruebas de vuelo real. También puede ser interesante si se dispone de la Raspberry Pi pero no del dron.   

Aquí puede encontrarse una [guía para la configuración de una Raspberry Pi](materiales_profesorado/configuracionRPi.pdf), aunque hay muchos tutoriales en internet que explican bien ese proceso. Lo importante es que, para implementar el esquema que proponemos aquí, es necesario que la Raspberry Pi esté conectada a la misma wifi que el portátil en el que estará ejecutándose el simulador SITL, de manera que cuando el autopiotService se conecte use como connection_string _'tcp:xxxxxxx:5763'_, siendo _xxxxxx_ la ip que tiene asignada el portátil en el que se ejecuta el SITL (que puede averiguarse con el comando de Windows _ipconfig_).






