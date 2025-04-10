## CONFIGURACIÓN DEL SENSOR DE MOVIMIENTO POR INFRARROJOS PASIVO (PIR):

En este apartado vamos a instalar y configurar el sensor que vamos a utilizar en nuestra ESP-32, el sensor de PIR o infrarrojo pasivo.

El primer paso es conectar físicamente nuestro sensor PIR a nuestra ESP-32. Para ello, deberemos seguir un esquema específico para no provocar errores en el dispositivo o en el sensor. Vamos a utilizar tres conectores, a los cuales vamos a darle un color específico para poder identificarlos de manera sencilla e inequívoca, a continuación resumiremos el esquema de colores que hemos utilizado:


### Identificación de conectores del sensor:

- Color Negro: El cable que está situado en el puerto izquiero de nuestro sensor y que está conectado al puerto de tierra de la ESP-32 (GND). Este es el primer cable que debemos conectar por seguridad.
  
- Color Verde: El cable situdado en el puerto central de nuestro sensor y que está conectado a uno de los puertos de información GPIO indicados en nuestra ESP-32 con una D como inicial (en nuestro modelo es D, aunque en otros modelos de ESP-32 podría ser E o G). En nuestro caso lo hemos conectado al puerto D2.
  
- Color Rojo: El cable situado en el puerto de la derecha de nuestro sensor y que está conectado al puerto de 5V (debido a que en nuestra ESP-32 no hay puerto de 5V, hemos optado por utilizar la protoboard, que hemos alimentado con un cable USB para conseguir que nos de los 5V), para dar energía a nuestro sensor. Hay que tener mucho cuidado, ya que este cable conectado en un puerto erróneo podría provocar el fundido del sensor.
