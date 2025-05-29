## COMUNICACION CON MQTT.

Lo primero que tendremos que hacer sera irnes en nuestro HomeAssitant a la parte de configuracion,buscando el apartado de complementos y presionando en el.


![image](https://github.com/user-attachments/assets/2c017f24-2a55-4506-a48a-61e715207778)


Una vez dentro presionaremos en la parte de abajo a la derecha donde pone **"tienda de complementos"**


![image](https://github.com/user-attachments/assets/a88c0e0c-32a9-4df0-97f2-be3e33e2a645)


Seguidamente en el navegador buscaremos la palabra **Mosquitto** y le daremos a instalar


![image](https://github.com/user-attachments/assets/30dec620-5bb2-4082-8c76-e218fcfab579)


Lo proximo es irnos a **EspHome Builder** y configurara nuestra **ESP32** para que funcione el **MQTT**


![image](https://github.com/user-attachments/assets/63100e19-eddf-490b-befd-012d99cd6484)


Una vez dentro indrocuciremos el siguiente codigo:


![image](https://github.com/user-attachments/assets/1d9b6c33-8b24-472b-838e-9de11a6f7d05)


#CONFIGURACION MQTT

mqtt:
  broker: "192.168.4.206"
  username: "jca_rec"
  password: "JCA"
  keepalive: 10s


Cuando hayamos escrito el codigo, le daremos a **"save"** y a **"instalar"**, e instalaremos el archivo **.yaml** como ya hemos hecho en todas estas ocasiones atras.


![image](https://github.com/user-attachments/assets/63309ced-1068-4aa6-8522-69bd69c8b656)

Una vez instalado, tendremos que irnos a nuestro movil, para poder mandar información desde nuestro móvil tendremos que descargarnos la siguiente aplicación:


