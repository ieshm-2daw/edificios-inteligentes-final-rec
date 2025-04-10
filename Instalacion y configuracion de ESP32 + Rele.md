##INSTALACION Y CONFIGURACION DE ESP32
El primer paso a seguir sera conectar nuestra **ESP32** al ordenador con el que vayamos a reconecer el dispositivo con un **cable USB**,
una vez conectado abriremos **Home Assistant en nuestro navegador** , introduciremos nuestro usuario,contraseña y nos iremos a  **ESPHome Builder**.

Una vez alli haremos click donde pone **NEW DEVICE**

![image](https://github.com/user-attachments/assets/0d5ea087-94cb-4fb7-95af-bad9166d7033)

Se abrira una ventana donde podremos configurar el nombre de nuestro dispositivo.Cuando lo hayamos introducido pulsamos Next:

![image](https://github.com/user-attachments/assets/a9acd7a7-0cd7-43e1-a91a-f21c360e053a)

Elegimos el dispositivo de la lista (en nuestro caso ESP32) y seguimos los pasos.Cuando terminemos la configuración del dispositivo 
saltará una ventana indicando la clave de encriptación y  pulsamos en Install:

![image](https://github.com/user-attachments/assets/8bc774df-0a1d-44f0-ba91-d7ea7606b90e)

![image](https://github.com/user-attachments/assets/8b581ecd-6ce3-4c9a-9ea5-ff71a60c8d16)


En la siguiente ventana , despues de pulsar install deberemos especificar cómo queremos instalar el archivo .yaml en el dispositivo.
Pulsaremos en la opcion **plug into this computer**

![image](https://github.com/user-attachments/assets/c89e8c0e-0ad6-4068-b6e8-bde5ca5e9d51)

Una vez pulsado nos parecera la siguiente pestaña , donde tendramos que esperar unos minutos a que prepare el archivo .yaml para poder
descargarlo.

![image](https://github.com/user-attachments/assets/536bd7f5-cc15-4de2-b3ab-0f4b1645df2b)

Le daremos a **OPEN ESPHOME WEB** y nos llevara a la siguiente pestaña:

![image](https://github.com/user-attachments/assets/db555434-55f8-4acb-b208-77d2aa859b75)

Pulsaremos en conectar y seleccionaremos la conexion usb de nuestro ordenador,una ve hecho se nos abrira la siguiente pestaña:

![alt text](image-1.png)

Presionaremos en seleccionar archivo,seleccionaremos el archivo **.yaml** descargado previamente y pulsaremos **instalar**.

![alt text](image-2.png)


switch:
 - platform: gpio
   name: "Relay"
   pin: GPIO19




