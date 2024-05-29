# Guía del profesor

## Ampliación de la librería dronLib
La librería que se ha usado en el taller (DronLib) está en desarrollo. En la versión disponible en el repositorio del taller tiene un mínimo conjunto de métodos, suficientes para los objetivos del taller. Pero naturalmente es posible ampliar en gran medida las funcionalidades de la librería. Este puede ser un proyecto interesante: organizar a los alumnos del curso en equipos y encargar a cada equipo que desarrolle algunas funcionalidades adicionales a la librería.    
      
No es un ejercicio fácil, porque hay que hacer una búsqueda de información sobre qué cosas pueden hacerse con la librería pymavlink que, aunque es fácil encontrar información sobre ella en internet, no es una librería fácil de usar. Por otra parte, hay que implementar después los nuevos métodos siguiendo la filosofía de DronLib (por ejemplo, implementando la versión bloqueante y la no bloqueante, cuando eso tenga sentido.     
     
Veamos un ejemplo que ilustra cómo habría que afrontar este reto. Supongamos que queremos añadir a la librería un método que nos permita leer los puntos del geofence, en el caso de que haya alguno cargado en el dron. Esto podría ayudarnos a mejorar las funcionalidades de la etapa 2A, añadiendo el código necesario para pintar en el mapa, después de la conexión con el dron, el geofence que ya esté cargado en el dron, si es que hay alguno.     
    
Esta funcionalidad requiere primero averiguar cuántos puntos tiene el geofence y luego leer uno a uno esos puntos para colocarlos en una lista y retornar esa lista al programa que llama a la función.     
     
El número de puntos del geofence es uno de los parámetros del dron: ‘FENCE_TOTAL’. En el taller ya se ha explicado cómo leer cualquiera de los parámetros. Por otra parte, después de un cierto esfuerzo de búsqueda para averiguar cómo pedir al dron los puntos del geofence veremos que eso puede hacerse enviando un mensaje de tipo MAVLink_fence_fetch_point_message, en el que, entre otros parámetros, se le indica el número de orden del punto que quiere leerse. Podemos ya imaginar un bucle en el que damos tantas vueltas como nos indique el valor del parámetro ‘FENCE_TOTAL’, de manera que en cada iteración recuperamos uno de los puntos del geofence y lo añadimos a la lista.
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
   
El código de este método hay que ubicarlo en alguno de los ficheros de la carpeta módulos. Lo correcto sería añadirlo al fichero dron_setGeofence.py, aunque tras esta incorporación quizá habría que cambiar el nombre a este fichero. Finalmente, hay que añadir los nombre de los nuevos métodos en el fichero Dron.py:    

```
from modules.dron_setGeofence import setGEOFence, _setGEOFence, getGEOFence, _getGEOFence
```
     
Naturalmente, el trabajo no puede dares por acabado sin haber hecho una prueba de que el nuevo método funciona correctamente, tanto en su versión bloqueante como en la no bloqueante. En el código de la etapa 2A sería fácil hacer una llamada inmediatamente después de haber creado el geofence, para comprobar que el nuevo método ha leído correctamente los puntos del geofence.

