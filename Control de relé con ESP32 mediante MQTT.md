## CONTROL DE RELÉ CON ESP32 MEDIANTE MQTT:

En este apartado vamos a instalar y configurar el módulo relé que vamos a utilizar con nuestra ESP32. Este módulo nos permitirá encender o agapar dispositivos eléctricos de forma remota, mediante comunicación MQTT desde una app móvil (IoT MQTT Panel) y gestionando a través de Home Assistant usando el broker Mosquitto.


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

En primer lugar, realizaremos una automatización para que cuando se reciba un mensaje predeterminado por MQTT, en este caso ON, se encianda nuestro Relé.

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


_Realizado por Alba Martín Díaz_
