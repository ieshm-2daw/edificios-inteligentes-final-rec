## INSTALACIÓN DEL ENTORNO:

### Identificación de componentes del Kit
- Placa ESP-32: Microcontrolador que puede controlar directamente sensores, actuadores y comunicarse con otros dispositivos a través de Wi-Fi o Bluetooth.
  
![image](https://github.com/user-attachments/assets/cea71652-a619-459f-9346-7b91aeb0535a)

- Placa desarrollo para ESP-32: Pequeña computadora de tamaño reducido, que te permite crear proyectos de electrónica y programación de forma sencilla. Incorpora un chip llamado ESP-32, que le permite de conectarse a internet a través de Wi-Fi y Bluetooth.

![image](https://github.com/user-attachments/assets/c54ba631-dcc8-4b8f-9e11-e5878c36bbd8)

- Cable de alimentación USB-C a USB: Cable que sirve como puente entre la fuente de alimentación (un PC, por ejemplo) y la placa de desarrollo ESP-32. Permite tanto alimentar la placa como programarla.
  
![image](https://github.com/user-attachments/assets/3ac0b501-66aa-4142-8899-060f247f5a2b)

- Sensor de gas CO2 TVOC CCS811: Componente electrónico diseñado para monitorear la calidad del aire en espacios cerrados. Es capaz de detectar dos tipos principales de contaminantes (CO2 y TVOC) basándose en el cambio de resistencia eléctrica a un material semiconductor en contacto con estos gases.
  
![image](https://github.com/user-attachments/assets/95b1e532-e82f-42a6-b7ec-deef299bf472)

- Sensor de iluminación BH1750: Componente electrónico diseñado para medir la intensidad de la luz presente en un espacio cerrado, al aire libre o en cualquier otro lugar. El sensor convierte la intensidad lumínica en señal eléctrica para poder procesarla y obtener mediciones.
  
![image](https://github.com/user-attachments/assets/701e5f25-6d3d-40a1-92b5-1b4597d8dc70)

- Sensor PIR (o infrarrojo pasivo): Dispositivo electrónico que detecta el movimiento de objetos que emiten calor, principalmente seres vivos. Funciona detectando cambios en la radiación infrarroja emitida por estos objetos.
  
![image](https://github.com/user-attachments/assets/5b4224f3-5e00-40e6-bfad-e3b19babfcec)

- Módulo RFID MRC522: Componente electrónico que permite a dispositivos como Raspberry Pi y otros microcontroladores leer y escribir datos en tarjetas RFID (Radio Frequency Identification) y etiquetas NFC. Al acercar una tarjeta al módulo, este envía una señal electromagnética que activa la tarjeta.
  
![image](https://github.com/user-attachments/assets/3cfd17ba-ed7d-4599-a8fe-49c3dd7c62ce)

- Sensor de corriente SCT-013 30A: Herramienta para monitorear y controlar el consumo eléctrico de dispositivos y circuitos que permite medir la corriente alterna que fluye por un conductor sin necesidad de interrumpir el circuito basándose en la inducción electromagnética.
  
![image](https://github.com/user-attachments/assets/8cd1b056-33c0-45cb-a4ff-db76f97ce367)

- Sensor de sonido KY-038: Componente electrónico diseñado para detectar y medir la intensidad del sonido en un entorno determinado. Capta las vibraciones del sonido por el micrófono, y si supera un determinado nivel se pone en alto (HIGH).
  
![image](https://github.com/user-attachments/assets/af24a6c1-f9e7-4671-8fae-15e9a70df06d)

- Sensor de movimiento microondas RCWL0516: Dispositivo electrónico que utiliza tecnología de microondas para detectar la presencia de objetos en movimiento. Detecta objetos hasta 5-7 metros de distancia, es inmune a corrientes de aire y puede detectar objetos a través de obstáculos no metálicos.

![image](https://github.com/user-attachments/assets/b6982525-4207-4b38-b187-e8b0e1b0cc37)

- Módulo de amplificación de señal LM358: Componente electrónico capaz de amplificar un pequeño voltaje y aumentar la amplitud de señales eléctricas débiles (como las de sensores o micrófonos) ajustando la ganancia en la tarjeta. La señal de salida será múltiplo de la señal de entrada.
  
![image](https://github.com/user-attachments/assets/d4c70117-8bf3-4109-b5f8-825c9d208188)

- Cerradura solenoide electromagnética: Tipo de cerradura eléctrica que utiliza un electroimán para controlar el mecanismo de bloqueo. Cuando se energiza la bobina, el centro de metal se mueve y hace que el solenoide sea capaz de tirar de un extremo.
  
![image](https://github.com/user-attachments/assets/9b3d9b4e-5c27-4865-8602-3c75e4d5811e)

- Módulo de relé optoacoplado 3V: Componente electrónico que actúa como un puente entre circuitos que operan a diferentes voltajes o que manejan tipos de señales distintas.
  
![image](https://github.com/user-attachments/assets/fd5a174b-ca95-43df-9bf5-726dcc4d1f4e)

- Protoboard 830 puntos C/MB102 (placa de pruebas): Herramienta que sirve como plataforma para montar circuito electrónicos de forma temporal y sin necesidad de soldar. Tiene orificios conductores que están conectados internamente en filas y columnas. Al insertar los componentes en estos orificios, se establecen conexiones eléctricas.
  
![image](https://github.com/user-attachments/assets/cdc1de20-9642-4aef-becb-8face368bdb7)

- Pantalla OLED 0.96"I2C: Pequeño dispositivo digital que permite mostrar texto, gráficos y pequeñas imágenes con buena calidad. Incorpora el controlador SDD1306 que nos permite una conexión I2C o SPI fácil de usar. Utilizan materiales orgánicos para emitir luz cuando se les aplica una corriente eléctrica.
  
![image](https://github.com/user-attachments/assets/60a5f1f3-595f-481c-8405-d1756f48c5ec)

- Raspberry Pi 5 4GB: Pequeño ordenador de placa única (SBC), desarrollada como un ordenador completo de tamaño reducido. Tiene un rendimiento muy bueno y permite ejecutar aplicaciones más exigentes y realizar tareas complejas de manera fluida. Cuenta con una gran variedad de puertos y conexiones, como puertos USB, Ethernet, salida HDMI y una ranura para tarjetas microSD.
  
![image](https://github.com/user-attachments/assets/fda0aee7-31fa-4b2e-9a74-2ca7af785e13)

- Carcasa con disipador Raspberry Pi 5: Disipador térmico que ayuda a extraer el calor del procesador y otros componentes críticos de la Raspberry Pi, manteniendo la temperatura bajo control y evitando fallos en el rendimiento, ampliando así la vida útil de la placa. Además, la protege de golpes, polvo y otros agentes externos.
  
![image](https://github.com/user-attachments/assets/f2006441-d1b4-4268-b387-059bb022af90)

- Fuente de alimentación 5.5V/5.1A USB-C: Fuente de alimentación que proporciona una corriente de 5.1 amperios a un voltaje de 5.5 voltios a través de un conector USB-C, suministrando la energía necesaria para alimentar dispositivos electrónicos que requieran esta especificación.
  
![image](https://github.com/user-attachments/assets/860303c7-5cb2-43c8-aa82-08047c2b34ff)

- Tarjeta MicroSD 32GB: Funciona como un pequeño disco duro para la Raspberry Pi. Es donde se almacena el sistema operativo, programas, archivos y proyectos.
  
![image](https://github.com/user-attachments/assets/42881f34-22b2-4411-8890-bfad3a92811b)


### Home Assistant
Es una plataforma de automatización del hogar de código abierto que permite controlar y monitorizar dispositivos inteligentes. Está diseñada para funcionar localmente, sin depender de la nube, y es compatible con una amplia variedad de dispositivos y servicios como luces, cámaras, termostatos, enchufes inteligentes, etc.

### Node-Red
Es una herramienta de programación visual que se implementa en dispositivos controladores de hardware, en nuestro caso en Raspberry Pi 5. Facilita la creación de flujos de trabajo entre diferentes dispositivos y servicios y muestra de manera visual las relaciones y funciones. Puede integrarse fácilmente con plataformas como Home Assistant con bases de datos como InfluxDB.

### ESPHome
Es una herramienta que lee un fichero de configuración y crea un firmware personalizado que posteriormente puedes subir a tus ESP32 o ESP8266, transformándolos en sensores inteligentes que pueden integrarse fácilmente en Home Assistant.

### Mosquitto Broker
Se trata de un servidor de mensajería de código abierto MQTT (versiones 3.1 y 3.1.1) que actúa como intermediario, permitiendo que diferentes dispositivos se comuniquen entre sí de forma eficiente y ligera. Es fundamental para sistemas IoT.

### InfluxDB
InfluxDB es una base de datos de series temporales diseñada para almacenar, consultar y analizar grandes volúmenes de datos que varían con el tiempo, como mediciones de sensores, métricas de rendimiento o datos de monitoreo. Es muy eficiente para manejar datos de alta frecuencia, ofreciendo consultas rápidas y almacenamiento optimizado para este tipo de datos. Utiliza InfluxQL como su lenguaje de consulta y es ideal para crear gráficas detalladas en Grafana.

### Grafana
Es una herramienta de visualización de datos con software libre (basado en licencia de Apache 2.0,2) que permite crear cuadros de mando y gráficos personalizados a partir de información almacenada en múltiples fuentes, incluidas bases de datos como InfluxDB.


### Instalación del software Raspberry Pi Imager
Raspberry Pi Imager es una herramienta que permite seleccionar e instalar sistemas operativos directamente en una tarjeta SD (o dispositivo USB) para poder utilizarlo en una Raspberry. Para iniciar la instalación, nos dirigimos a la página web oficial de Raspberry: https://www.raspberrypi.com/software/
En la pantalla de inicio nos encontraremos un instalador, tendremos que seleccionar el link de descarga correspondiente al sistema operativo de nuestro PC. En nuestro caso Windows:

![image](https://github.com/user-attachments/assets/ca31f4e7-3141-43e3-938f-c0406f5f6d10)

Una vez descargado el archivo .exe lo abrimos y vamos siguiendo los pasos indicados por el programa de instalación (Pulsar el botón Install y por último Finish):

![image](https://github.com/user-attachments/assets/a7a91c64-cde0-4579-ac7d-4968b0ad9a66)

Antes de continuar la instalación, debemos tener una tarjeta SD en el dispositivo que tiene instalado el programa de Raspberry Pi Imager, será la forma de transportar los programas a nuestra Raspberry.

Una vez instalado y conectada la tarjeta SD, ejecutamos el programa y nos debería salir la siguiente pantalla:

![image](https://github.com/user-attachments/assets/d20fdf84-cb18-470b-9986-25cb0899730d)

En ella, seleccionamos el nombre del dispositivo en el que vamos a instalar los programas, en este caso utilizaremos la Raspberry Pi 5. A continuación, seleccionaremos el sistema operativo, para ello pulsaremos en el botón de ELEGIR SO y seguiremos la ruta:

**Other specific-purpose OS -> Home Assistant and home automation -> Home Assistant**

y seleccionamos el Home Assistant que aparece en la lista.

En el apartado de almacenamiento, deberemos seleccionar nuestra tarjeta SD previamente introducida en nuestro ordenador. Pulsamos siguiente y seguimos los pasos de instalación.

![image](https://github.com/user-attachments/assets/d59214e6-25d9-4c3d-8f49-345d464a8106)

Al final del proceso nos mostrará la información en una nueva pestaña:

![image](https://github.com/user-attachments/assets/bb53c680-5278-464a-8fcc-d3d564f214a1)

A continuación, conectamos la tarjeta a la Raspberry Pi y la iniciamos. Deberemos esperar a que la configuración se complete. Una vez configurada, si conectamos la Raspberry Pi a una pantalla debería aparecernos algo similar a esto. con la información del dispositivo en Home Assistant:

![HomeAssistant](https://github.com/user-attachments/assets/99a848e2-1f3f-47af-b5ea-8ea6402e4fee)

Por último, desde Home Assistant, instalamos los complementos que necesitemos. En nuestro caso serán: ESPHome, Grafana, InfluxDB y Node-Red.

![Captura desde 2025-03-27 10-25-02](https://github.com/user-attachments/assets/d8f28504-7e3e-4aee-b5f2-7e54fb79c578)

![Captura desde 2025-03-27 10-25-19](https://github.com/user-attachments/assets/55e082e3-067a-49d4-a3eb-096a23950a18)

![Captura desde 2025-03-27 10-25-34](https://github.com/user-attachments/assets/e827cf96-387e-486c-b28d-5978afeb82f7)

![Captura desde 2025-03-27 10-25-45](https://github.com/user-attachments/assets/423c43fa-dd85-4009-a540-c8e0037e0bfc)

![Captura desde 2025-03-27 10-28-09](https://github.com/user-attachments/assets/6a54d243-5bde-4c49-b8ab-3cce606e580d)


### Instalación de ESP-32 en ESPHome:
Una vez realizado todo lo anterior, ahora pasaremos a instalar nuestra ESP-32 en ESPHome, para poder programarla.

El primer paso es irnos al apartado ESPHome Builder de nuestro Home Assistant y una vez ahí pulsaríamos en el botón de "NEW DEVICE".

<a href="https://github.com/user-attachments/assets/3c1ef015-356e-4949-9496-523c853e09fe" target="_blank">Haz clic para ver la imagen</a>

A continuación, nos aparecerá un cuadro de diálogo en el cuál tendremos que pulsar sobre el botón que dice "OPEN ESPHOME WEB".

<a href="https://github.com/user-attachments/assets/444ba8bd-4e1c-438f-a270-9f9e523b7842" target="_blank">Haz clic para ver la imagen</a>

Una vez hecho esto, se nos abrirá una pestaña en el navegador en la cual nos aparecerá el ESP Device como no conectado, y debajo un botón "CONNECT", nosotros pulsaremos dicho botón.

<a href="https://github.com/user-attachments/assets/0a3bf87b-7bbb-484f-856b-5e985832b77c" target="_blank">Haz clic para ver la imagen</a>

Una vez que pulsamos el botón, se nos abrirá una ventana que nos solicitará conectarse a un puerto serie, generalmente el nuestro será el último de la lista "USB Serial".

<a href="https://github.com/user-attachments/assets/b7f9f99a-72d8-434b-b37a-b396e5b9fd02" target="_blank">Haz clic para ver la imagen</a>

Cuando le damos a la opción correcta, en la web ahora nos aparecerá el ESP Device como "CONNECTED" y ahora tendríamos que pulsar donde nos dice "PREPARE FOR FIRST USE".

<a href="https://github.com/user-attachments/assets/80e85891-939f-4230-883e-1137bd65b975" target="_blank">Haz clic para ver la imagen</a>

Una vez que hemos pulsado sobre dicha opción se nos abrirá un cuadro de texto en el que tendremos que pulsar sobre "INSTALL".

<a href="https://github.com/user-attachments/assets/62dc1fb0-54f1-463c-bc6f-35001b886a8d" target="_blank">Haz clic para ver la imagen</a>

Una vez que hemos hecho esto y nos hemos descargado el archivo que nos ha proporcionado, ahora tendremos que pulsar sobre "INSTALL".

<a href="https://github.com/user-attachments/assets/80e85891-939f-4230-883e-1137bd65b975" target="_blank">Haz clic para ver la imagen</a>

Después de pulsar sobre "INSTALL" se nos abrirá de nuevo una ventanita en la que nos dará la opción de cargar un archivo, aquí deberemos cargar el archivo que nos hemos descargado en el paso anterior, y una vez instalado esto, ya estaría disponible para funcionar correctamente.

<a href="https://github.com/user-attachments/assets/c1915c55-86cc-41f5-9fd1-27a1d21e684d" target="_blank">Haz clic para ver la imagen</a>



_Realizado por Alba Martín Díaz_
