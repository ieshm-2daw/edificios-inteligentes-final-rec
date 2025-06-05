# Sistema de Domotización con ESP32, RFID y MQTT

## Introducción

Este proyecto describe la implementación de un sistema de domotización que permite controlar el encendido y apagado de un PC utilizando un sensor RFID para autenticación y un relé para el control físico. Además, se integra MQTT para permitir el monitoreo y control remoto desde una aplicación móvil, con restricciones de seguridad basadas en un temporizador de autenticación.


## Objetivo del Proyecto

El objetivo principal es crear un sistema de domotización que permita controlar el encendido y apagado de un PC de manera segura utilizando una tarjeta RFID para autenticación física y una aplicación móvil para control remoto, todo ello gestionado a través de un ESP32 y comunicado mediante MQTT.


## Componentes Necesarios

- **ESP32**: Actúa como el cerebro del sistema, gestionando la lógica de control, la comunicación con el sensor RFID, el relé y el broker MQTT.
- **Sensor RFID RC522**: Utilizado para autenticar al usuario mediante una tarjeta RFID específica. Solo la tarjeta autorizada puede activar o desactivar el sistema.
- **Relé**: Componente físico que nos permitirá encender o apagar el PC. El relé será controlado por el ESP32.
- **Tarjeta RFID**: Configurada para ser reconocida por el sistema.
- **Broker MQTT**: Facilita la comunicación entre el ESP32 y la aplicación móvil. En este caso, utilizaremos Mosquitto integrado en Home Assistant.
- **Aplicación MQTT para Móvil**: IoT MQTT Panel nos permite monitorizar y controlar el estado del relé desde su móvil, siempre y cuando se haya autenticado previamente con la tarjeta RFID.


## Lógica de Funcionamiento
## Autenticación con RFID
- **Detección de la tarjeta RFID**: Cuando el sensor RFID detecte la tarjeta autorizada, enviará una señal al ESP32.
- **Activación del relé**: El ESP32 activará el relé, lo que encenderá el PC.
- **Modo autorizado**: Al detectar la tarjeta, el ESP32 activa un "modo autorizado" que permite el control remoto a través de MQTT durante un periodo de 8 horas.

```
binary_sensor:
  - platform: rc522
    uid: F3-B6-69-30  # UID de la tarjeta RFID autorizada
    name: "RC522 RFID Tag"
    on_press:
      then:
        - if:
            condition:
              lambda: 'return id(authorized_mode);'
            then:
              - switch.turn_off: relay_control
              - globals.set:
                  id: authorized_mode
                  value: 'false'
            else:
              - switch.turn_on: relay_control
              - globals.set:
                  id: authorized_mode
                  value: 'true'
              - delay: 8h
              - globals.set:
                  id: authorized_mode
                  value: 'false'

```


## Temporizador de Autenticación
- **Iniciar temporizador**: Una vez autenticado con la tarjeta RFID, se inicia un temporizador de 8 horas. Durante este tiempo, el usuario puede controlar el relé desde la aplicación móvil.
- **Finalización del temporizador**: Después de 8 horas, el "modo autorizado" se desactiva automáticamente, y el usuario debe volver a autenticarse con la tarjeta RFID para reactivar el control remoto.


```
on_press:
  then:
    - switch.turn_on: relay_control
    - globals.set:
        id: authorized_mode
        value: 'true'
    - delay: 8h
    - globals.set:
        id: authorized_mode
        value: 'false'
```

## Comunicación MQTT
- **Publicación de estados**: El ESP32 publica el estado del relé (encendido/apagado) en un tema MQTT (2daq/relay/state) cada vez que cambia el estado.
- **Suscripción a comandos**: El ESP32 está suscrito a un tema MQTT (2daw/relay/command) para recibir comandos desde la aplicación móvil. Solo actúa sobre estos comandos si el "modo autorizado" está activo.


```
mqtt:
  broker: "192.168.4.206"
  username: "jca_rec"
  password: "JCA"
  port: 1883
  on_message:
    topic: "2daw/relay/command"
    then:
      - if:
          condition:
            lambda: 'return id(authorized_mode) && payload == "ON";'
          then:
            - switch.turn_on: relay_control
      - if:
          condition:
            lambda: 'return payload == "OFF";'
          then:
            - switch.turn_off: relay_control
```


## Interacción entre componentes
1. **Autenticación inicial**: El usuario pasa la tarjeta RFID autorizada frente al sensor.
2. **Activación del relé**: El ESP32 activa el relé, encendiendo el PC, y activa el "modo autorizado".
3. **Control remoto**: Durante las siguientes 8 horas, el usuario puede enviar comandos MQTT desde la aplicación móvil para controlar el relé.
4. **Finalización del modo autorizado**: Después de 8 horas, el "modo autorizado" se desactiva, y el usuario debe volver a autenticarse con la tarjeta RFID para reactivar el control remoto.


## Consideraciones de seguridad:
- **Autenticación en dos pasos**: El control remoto solo es posible después de una autenticación física con la tarjeta RFID.
- **Cifrado MQTT**: Se recomienda usar MQTT con cifrado (por ejemplo, MQTT sobre TLS) para asegurar la comunicación entre el ESP32 y el broker.
- **Red local segura**: Asegurar que la red local está protegida para evitar accesos no autorizados.

## Conexiones

### Conexión del Sensor RFID RC522 al ESP32

| Pin RC522 | Pin ESP32 |
|-----------|-----------|
| SCK       | GPIO18    |
| MOSI      | GPIO23    |
| MISO      | GPIO19    |
| SS        | GPIO5     |

### Conexión del Relé al ESP32

- **Pin de control del relé**: Conectado a GPIO17 del ESP32.
- **Alimentación del relé**: Conectada a la fuente de alimentación del PC.

## Configuración del Software

### Configuración del ESP32 con ESPHome

```
esphome:
  name: esp32-alba
  friendly_name: ESP32_alba

esp32:
  board: esp32dev
  framework:
    type: arduino

logger:

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  ap:
    ssid: "Esp32-Alba Fallback Hotspot"
    password: "ap927zoWd11T"

captive_portal:

globals:
  - id: authorized_mode
    type: bool
    initial_value: 'false'

spi:
  clk_pin: GPIO18
  mosi_pin: GPIO23
  miso_pin: GPIO19

rc522_spi:
  cs_pin: GPIO5
  update_interval: 1s

binary_sensor:
  - platform: rc522
    uid: F3-B6-69-30  # UID de tu tarjeta RFID autorizada
    name: "RC522 RFID Tag"
    on_press:
      then:
        - if:
            condition:
              lambda: 'return id(authorized_mode);'
            then:
              - switch.turn_off: relay_control
              - globals.set:
                  id: authorized_mode
                  value: 'false'
              - mqtt.publish:
                  topic: "2daw/relay/state"
                  payload: "OFF"
            else:
              - switch.turn_on: relay_control
              - globals.set:
                  id: authorized_mode
                  value: 'true'
              - delay: 8h
              - globals.set:
                  id: authorized_mode
                  value: 'false'
              - mqtt.publish:
                  topic: "2daw/relay/state"
                  payload: "ON"

switch:
  - platform: gpio
    name: "Relay"
    pin: GPIO17
    id: relay_control
    on_turn_on:
      then:
        - if:
            condition:
              lambda: 'return id(authorized_mode);'
            then:
              - mqtt.publish:
                  topic: "2daw/relay/state"
                  payload: "ON"
    on_turn_off:
      then:
        - mqtt.publish:
            topic: "2daw/relay/state"
            payload: "OFF"

mqtt:
  broker: "192.168.4.206"  # Dirección IP de tu broker MQTT
  username: "jca_rec"  # Credenciales si son necesarias
  password: "JCA"
  port: 1883
  on_message:
    topic: "2daw/relay/command"
    then:
      - if:
          condition:
            lambda: 'return id(authorized_mode) && payload == "ON";'
          then:
            - switch.turn_on: relay_control
      - if:
          condition:
            lambda: 'return payload == "OFF";'
          then:
            - switch.turn_off: relay_control
```

(A continuación se presentan los informes realizados previamente, que detallan la correcta conexión y configuración tanto del módulo RFID con el relé, como la conexión y comunicación mediante MQTT con Home Assistant.)

## CONFIGURACIÓN DEL MÓDULO RFID MRC522:

En este apartado vamos a instalar y configurar el módulo que vamos a utilizar en nuestra ESP-32, el módulo RFID, más concretamente el modelo MRC522.

El primer paso es conectar físicamente nuestro módulo RFID a nuestra ESP-32. Para ello, deberemos seguir un esquema específico para no provocar errores en el dispositivo o en el módulo. Para conectar nuestro módulo RFID vamos a utilizar una protoboard, aunque hay que tener en cuenta que en algunos dispositivos puede ser necesario soldar los pines a la placa. El esquema que vamos a utilizar para conectar a la ESP-32 es el siguiente:


## Identificación de conectores del sensor:

Para guiarnos sobre dónde tenemos que situar los cables conforme a la dispsición de nuestros conectores, siempre utilizaremos como referencia la siguiente imagen:

<a href="https://github.com/user-attachments/assets/a9237bb0-49b5-4bff-bfff-3a3ab0509a8b">
  <img src="https://github.com/user-attachments/assets/a9237bb0-49b5-4bff-bfff-3a3ab0509a8b" width="300"/>
</a>

Los cables quedarían de la siguiente forma:

<a href="https://github.com/user-attachments/assets/c3d0be61-46b2-41c9-9343-b4257bbed3d5">
  <img src="https://github.com/user-attachments/assets/c3d0be61-46b2-41c9-9343-b4257bbed3d5" width="300"/>
</a>


- Color Blanco: Este cable está conectado al puerto SDA del módulo, que en nuestro ESP-32 corresponde al pin D5 (GPIO5). Este cable es responsable de la transmisión de datos en protocolos de comunicación como I2C, por lo que es fundamental asegurarse de que esté bien conectado para garantizar una correcta comunicación entre el módulo y la placa.

- Color Naranja: Este cable corresponde al pin SCK del módulo, y en nuestra ESP-32 lo hemos conectado al pin D18 (GPIO18). El pin SCK (Serial Clock) se encarga de sincronizar la comunicación SPI entre dispositivos, actuando como señal de reloj.

- Color Amarillo: Este cable conectado al puerto MOSI del módulo y al pin D23 (GPIO23) de nuestra ESP-32.
MOSI (Master Out Slave In) es el canal por el cual el microcontrolador (ESP-32) envía datos hacia el módulo. Es crucial que este cable esté correctamente conectado para asegurar que el módulo reciba las instrucciones adecuadas.

- Color Azul: Este cable se conecta al pin MISO del módulo y al pin D19 (GPIO19) de la ESP-32. MISO (Master In Slave Out) es el canal por el cual el módulo devuelve información al microcontrolador. Sin este cable, no podríamos recibir datos desde el módulo.

- Color Negro: Este cable se encuentra conectado al pin GND del módulo, y va también al puerto GNID de nuestra ESP-32. Es fundamental realizar esta conexión en primer lugar para establecer una referencia común de voltaje y evitar posibles daños por diferencias de potencial.

- Color Rojo: Este cable alimenta el módulo con energía eléctrica. En este caso, lo hemos conectado al pin de 3.3V de la ESP-32, ya que el módulo está diseñado para trabajar con este voltaje. Conectarlo a un voltaje superior podría dañar permanentemente el módulo.

<div align="center">
  
| Colores           | Negro | Blanco | Naranja | Amarillo | Azul  | Rojo |
|-------------------|--------|--------|---------|----------|-------|------|
| Puerto del Módulo | GND    | SDA    | SCK     | MOSI     | MISO  | 3.3V |
| ESP32             | GND    | D5     | D18     | D23      | D19   | 3V   |

</div>


## Configuración en ESPHome:

Una vez que ya tenemos conectado nuestro módulo con nuestra ESP-32 físicamente, pasamos a configurar el sensor para poder realizar acciones con él. Para esto, nos dirigimos a la página principal de Home Assistant y entramos en ESPHome, aquí editaremos nuestro archivo .yaml y añadiremos todo el código necesario para que nuestro módulo sea reconocido por nuestra ESP-32 y sea funcional. En nuestro caso nos hemos remitido a la propia web oficial de ESPHome, donde nos dan toda la información y código necesarios para la configuración de nuesto módulo (https://esphome.io/components/binary_sensor/rc522.html). Aquí debajo se muestra el código que nos proporciona la propia página, quedando únicamente que cambiar los apartados "_pin:" por los que hemos designado físicamente (posteriormente, una vez que hagamos la primera interacción con los dispositivos nfc que trae el propio módulo, cambiaremos también el apartado "uid:" con el que nos saldrá en los logs).

```
spi:
  clk_pin: D0
  miso_pin: D1
  mosi_pin: D2

rc522_spi: # or rc522_i2c
  cs_pin: D3
  update_interval: 1s

binary_sensor:
  - platform: rc522
    uid: 74-10-37-94
    name: "RC522 RFID Tag"
```


Ya sólo nos quedaría guardar e instalar nuestro nuevo archivo actualizado, lo haremos con la opción Wirelessly para que nos esa más fácil y rápido, aunque también es posible cargarlo manualmente por USB.

Así es como quedaría definitivamente nuestro código funcional:

```
spi:
  clk_pin: GPIO18
  mosi_pin: GPIO23
  miso_pin: GPIO19

rc522_spi:
  cs_pin: GPIO5
  update_interval: 1s

binary_sensor:
  - platform: rc522
    uid: F3-B6-69-30
    name: "RC522 RFID Tag"
```


## Aplicación del módulo RC522:

Este módulo, además de ser económico y confiable, tiene múltiples aplicaciones en proyectos de domótica escolar, entre ellas:

- Control de acceso: Abrir cerraduras inteligentes con tarjetas.

- Registro de asistencia: Gestionar la entrada y salida de alumnos y profesores.

- Activación automática de sistemas: Encender luces, sensores o equipos al detectar una tarjeta.

- Personalización del entorno: Adaptar la configuración del aula al usuario que accede.

- Gestión de préstamos de material: Registrar quién toma y devuelve dispositivos o recursos.

- Automatización de proyectos escolares: Asignar tareas, formar equipos y registrar progreso.

- Notificaciones de seguridad: Alertar si se abre la puerta o se queda vacía el aula.

- Acceso a contenido educativo: Desbloqueo automático de archivos o exámenes al pasar una tarjeta.



## Imágenes y vídeo:

A continuación se muestran las imágenes y vídeos extraídos del proceso de configuración y montaje de nuestro módulo:

<a href="https://github.com/user-attachments/assets/fa8f79e4-512a-40b6-a6bd-a6c5ee00e72e">
  <img src="https://github.com/user-attachments/assets/fa8f79e4-512a-40b6-a6bd-a6c5ee00e72e" width="300"/>
</a>

<a href="https://github.com/user-attachments/assets/7e69f6f1-e823-4d46-9433-8b0ac443b7e8">
  <img src="https://github.com/user-attachments/assets/7e69f6f1-e823-4d46-9433-8b0ac443b7e8" width="300"/>
</a>

<a href="https://github.com/user-attachments/assets/7eff329c-432f-44d1-8bc4-c4711f4852d2">
  <img src="https://github.com/user-attachments/assets/7eff329c-432f-44d1-8bc4-c4711f4852d2" width="300"/>
</a>

<a href="https://github.com/ieshm-2daw/edificios-inteligentes-final-rec/blob/main/M%C3%B3dulo%20RFID%20MRC522.mp4" target="_blank">Haz clic aquí para ir al enlace al video</a>


## Automatización:

Por último he creado una automatización para probar el funcionamiento de nuestro módulo combinado con un relé. La automatización en sí consiste en que si nuestro módulo recibe una lectura del NFC correspondiente, el relé alternará de estado, encendiéndose o apagándose dependiendo del estado original de este.

<a href="https://github.com/user-attachments/assets/b08d7ab9-a350-402d-a224-a0ca86f9395a">
  <img src="https://github.com/user-attachments/assets/b08d7ab9-a350-402d-a224-a0ca86f9395a" width="300"/>
</a>

<a href="https://github.com/user-attachments/assets/00a51d68-f697-4d23-a7b4-4c67d1463466">
  <img src="https://github.com/user-attachments/assets/00a51d68-f697-4d23-a7b4-4c67d1463466" width="300"/>
</a>

<a href="https://github.com/user-attachments/assets/15eee5e3-2011-4891-abf3-735436dbf00a">
  <img src="https://github.com/user-attachments/assets/15eee5e3-2011-4891-abf3-735436dbf00a" width="300"/>
</a>


## CONTROL DE RELÉ CON ESP32 MEDIANTE MQTT:

En este apartado vamos a instalar y configurar el módulo relé que vamos a utilizar con nuestra ESP32. Este módulo nos permitirá encender o apagar dispositivos eléctricos de forma remota, mediante comunicación MQTT desde una app móvil (IoT MQTT Panel) y gestionando a través de Home Assistant usando el broker Mosquitto.


## Instalación del complemento:

Lo primero será instalar el complemento de Mosquitto Broker, para ello nos dirigiremos a la pestaña Configuración de nuestro Home Assistant y entraremos al apartado de Complementos. Una vez aquí pulsaremos en el botón que aparece abajo a la derecha que pone Tienda de Complementos. Aquí nos dirigiremos al buscador y simplemente con poner mq nos aparecerá el complemento de Mosquitto Broker, una vez encontrado sólo tendriamos que instalarlo y ya lo tendríamos listo para poder utilizarlo.

<a href="https://github.com/user-attachments/assets/5bf1e194-4b50-4869-9584-e223e14549fe">
  <img src="https://github.com/user-attachments/assets/5bf1e194-4b50-4869-9584-e223e14549fe" width="300"/>
</a>
<a href="https://github.com/user-attachments/assets/ba137d6c-3610-4be3-8330-873e6cb77953">
  <img src="https://github.com/user-attachments/assets/ba137d6c-3610-4be3-8330-873e6cb77953" width="300"/>
</a>
<a href="https://github.com/user-attachments/assets/ca51d038-ee65-4bf0-8862-3b850fc0270b">
  <img src="https://github.com/user-attachments/assets/ca51d038-ee65-4bf0-8862-3b850fc0270b" width="300"/>
</a>


## Configuración de MQTT con ESPHome Builder:

Lo siguiente será realizar la configuración de nuestra ESP32 para que funcione con MQTT, como siempre, nos vamos ESPHome Builder y en nuestra ESP32 pulsamos en EDIT para agregar el código necesario para la configuración de MQTT.

```
switch:
  - platform: gpio
    name: "Relay"
    pin: GPIO18
    id: relay_mqtt
    on_turn_on:
      mqtt.publish:
        topic: "2daw/luz"
        payload: "ON"
    on_turn_off:
      mqtt.publish:
        topic: "2daw/luz"
        payload: "OFF"

mqtt:
  broker: "192.168.4.206"
  username: "jca_rec"
  password: "JCA"
  port: 1883
```

Lo guardamos, instalamos y ya lo tendríamos en funcionamiento.


## Instalación de Aplicación y manejo de MQTT desde el móvil:

En este caso, para poder mandar y recibir información a través de MQTT desde nuestro móvil, tendremos que descargarnos la siguiente aplicación:

<a href="https://github.com/user-attachments/assets/92e65804-73ec-4a84-aa2b-ed65ae81730e">
  <img src="https://github.com/user-attachments/assets/92e65804-73ec-4a84-aa2b-ed65ae81730e" width="300"/>
</a>

Una vez que la hemos instalado, lo primero que tendremos que hacer es introducir los datos para conectar la aplicación a nuestro Home Assistant.

<a href="https://github.com/user-attachments/assets/555b8e9c-1999-4192-9c09-7c2dbb004912">
  <img src="https://github.com/user-attachments/assets/555b8e9c-1999-4192-9c09-7c2dbb004912" height="300"/>
</a>

Después tendremos que configurar el Relé para poder activarlo y desactivarlo desde nuestro terminal.

<a href="https://github.com/user-attachments/assets/2fd43bfe-33e8-4149-a05e-6bccf34b2bf8">
  <img src="https://github.com/user-attachments/assets/2fd43bfe-33e8-4149-a05e-6bccf34b2bf82" height="300"/>
</a>


Topic: Lo hemos configurado anteriormente en nuestro archivo YAML por lo que sería 2daw/luz.

Payload_on: Mandará ON cuando se encienda.

Payload_off: Mandará OFF cuando se apague.


## Automatizaciones:

A continuación, pasaremos a realizar las correspondientes automatizaciones con las que conseguiremos interactuar con nuestro relé tanto desde el PC como desde nuestro terminal móvil.

En primer lugar, realizaremos una automatización para que cuando se reciba un mensaje predeterminado por MQTT, en este caso ON, se encienda nuestro Relé.

<a href="https://github.com/user-attachments/assets/13fb85c6-146d-4259-968e-f964a88a833a">
  <img src="https://github.com/user-attachments/assets/13fb85c6-146d-4259-968e-f964a88a833a" width="300"/>
</a>

Posteriormente, crearemos otra, para que cuando reciba el mensaje OFF por MQTT, el Relé se apague.

<a href="https://github.com/user-attachments/assets/8c5bfdcc-b830-4c3e-95cb-2dfc5eb724a0">
  <img src="https://github.com/user-attachments/assets/8c5bfdcc-b830-4c3e-95cb-2dfc5eb724a0" width="300"/>
</a>

Aprovechando que anteriormente realizamos la integración del Relé con el módulo RFID, también hemos realizado una automatización, para que cuando el sensor detecte su tag correspondiente, publique un mensaje MQTT que recibirá nuestro Relé y se encenderá o apagará dependiendo del mensaje que publique.

<a href="https://github.com/user-attachments/assets/1a19bd52-c150-4b59-bb18-39be7e29d4b1">
  <img src="https://github.com/user-attachments/assets/1a19bd52-c150-4b59-bb18-39be7e29d4b1" width="300"/>
</a>
<a href="https://github.com/user-attachments/assets/081c013f-17e6-47b6-bacc-c7ea94875e31">
  <img src="https://github.com/user-attachments/assets/081c013f-17e6-47b6-bacc-c7ea94875e31" width="300"/>
</a>
