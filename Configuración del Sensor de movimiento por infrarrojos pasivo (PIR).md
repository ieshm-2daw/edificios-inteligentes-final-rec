## CONFIGURACIÓN DEL SENSOR DE MOVIMIENTO POR INFRARROJOS PASIVO (PIR):

En este apartado vamos a instalar y configurar el sensor que vamos a utilizar en nuestra ESP-32, el sensor de PIR o infrarrojo pasivo.

El primer paso es conectar físicamente nuestro sensor PIR a nuestra ESP-32. Para ello, deberemos seguir un esquema específico para no provocar errores en el dispositivo o en el sensor. Vamos a utilizar tres conectores, a los cuales vamos a darle un color específico para poder identificarlos de manera sencilla e inequívoca, a continuación resumiremos el esquema de colores que hemos utilizado:


### Identificación de conectores del sensor:

- Color Negro: El cable que está situado en el puerto izquiero de nuestro sensor y que está conectado al puerto de tierra de la ESP-32 (GND). Este es el primer cable que debemos conectar por seguridad.
  
- Color Verde: El cable situdado en el puerto central de nuestro sensor y que está conectado a uno de los puertos de información GPIO indicados en nuestra ESP-32 con una D como inicial (en nuestro modelo es D, aunque en otros modelos de ESP-32 podría ser E o G). En nuestro caso lo hemos conectado al puerto D2.
  
- Color Rojo: El cable situado en el puerto de la derecha de nuestro sensor y que está conectado al puerto de 5V (debido a que en nuestra ESP-32 no hay puerto de 5V, hemos optado por utilizar la protoboard, que hemos alimentado con un cable USB para conseguir que nos de los 5V), para dar energía a nuestro sensor. Hay que tener mucho cuidado, ya que este cable conectado en un puerto erróneo podría provocar el fundido del sensor.

![1000082228](https://github.com/user-attachments/assets/878165b0-00ae-4e33-9992-1f72dabe4183)

![1000082229](https://github.com/user-attachments/assets/8f7947d8-c6bf-418f-9fb6-747a4e66b16a)


Una vez que ya tenemos conectado nuestro sensor con nuestra ESP-32 físciamente, pasamos a configurar el sensor para poder realizar mediciones con él. Para esto, nos dirigimos a la página principal de Home Assistant y entramos en ESPHome, aquí editaremos nuestro archivo .yaml y añadiremos todo el código necesario para que nuestro sensor sea reconocido por nuestra ESP32 y sea funcional. En nuestro caso nos hemos remitido a la propia web oficial de Home Assistant, donde nos dan toda la información y código necesarios para la configuración de nuestro sensor (https://devices.esphome.io/devices/Generic-PIR). Aquí debajo se muestra el código que nos proporciona la propia página, quedando únicamente que cambiar el apartado "pin:" y añadiendo el pin que hemos elegido en la configuración física, en nuestro caso el GPIO02.

![image](https://github.com/user-attachments/assets/cb17c46d-8450-441c-aee2-e10b4f4a2a6b)

Ya sólo nos quedaría guardar e instalar nuestro nuevo archivo actualizado, lo haremos con la opción Wirelessly para que nos sea más fácil y rápido, aunque también podríamos hacerlo de forma manual. Cuando ya hemos realizado todos los pasos anteriores, al dirigirnos al panel principal podremos ver que nuestro sensor ya se encuentra operativo y recibiendo las interacciones correspondientes.


### Ajuste del comportamiento del sensor:

Normalmente, estos sensores tienen dos potenciómetros (ruedita) que permiten regular:

1. Sensibilidad (SENS):
   - Ajusta cuán sensible es el sensor al movimiento.
   - Si la aumentas, el sensor puede detectar movimiento a mayor distancia o con menos movimiento.
   - Si la disminuyes, el sensor necesita un movimiento más fuerte o más cercano para activarse.

2. Tiempo de activación (TIME):
   - Controla cuánto tiempo permanece activa la señal de salida (por ejemplo, cuánto tiempo se mantiene encendido un LED o activado un relé).
   - Puede ir desde unos pocos segundos hasta varios minutos, dependiendo del sensor.


### ¿Cómo saber cuál es cuál?

Muchos sensores tienen marcas como "TIME" y "SENS" al lado de las ruedecitas. Si no están marcadas, puedes hacer una prueba:
- Mueve una rueda completamente a un lado, activa el sensor y observa.
- Si el tiempo cambia, es TIME. Si cambia la distancia de detección, es SENS.
