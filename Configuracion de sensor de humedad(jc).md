##Instalacion y configuracion del sensor de humedad.

Lo primero que tendremos que hacer sera **conectar el sensor de humedad y temperatura** a nuestra **ESP32** mediante nuestra **protoboard**.

Para ello tendremos que conectar el puerto de 3.3v de nuestra ESP32 a la linea de positivo de nuestra protoboard,lo siguiente sera conectar de nuestra ESP32 el tierra al negativo de nuestra protoboard.El sensor de **humedad** se conectara a nuestra protoboard de la siguiente forma,conectando el pin de **VCC** al 3,3v de nestra protoboard (**el positivo**), el **GND** lo conectaremos al **negativo** y el pin de **DATA** a un puerto cualquiera de nuestra **ESP32** , que no sea ni tierra ni 3,3v.

![IMG20250424105404](https://github.com/user-attachments/assets/9f0f28a1-d377-4959-adff-066f3880555a)


Ahora nos iremos a nuestro HomeAssitant , en el apartado de **ESPHome Builder** y le daremos a edit en nuestra **ESP32**.Una vez dentro tendremos que poner el siguiente codigo:

![image](https://github.com/user-attachments/assets/b5ac3b13-bc34-4227-a64f-7087bf74b86a)

![image](https://github.com/user-attachments/assets/ed6aa6d3-a31a-4096-9ea8-b0c0b231e1c7)


Una vez hecho le daremos a **Save** y a **install**, una vez hecho esto seguiremos descargando el archivo .yaml e instalandolo como hicimos anteriormente en la isntalacion del **ESP32**.

Esto seria un breve resumen:

En la siguiente ventana, después de pulsar install debemos especificar cómo queremos instalar el archivo .yaml en el dispositivo. Pulsaremos en la opción conectar a esta computadora

![image](https://github.com/user-attachments/assets/c370e0e0-8a1a-42d8-8063-2ec6b666847a)

Una vez pulsado nos parecerá la siguiente pestaña, donde tendremos que esperar unos minutos a que prepare el archivo .yaml para poder descargarlo.

![image](https://github.com/user-attachments/assets/b903edf2-7b43-4113-bd10-3b6d3f57ee7e)

Le daremos a OPEN ESPHOME WEB y nos llevara a la siguiente pestaña:

![image](https://github.com/user-attachments/assets/f51116da-3ac1-4de1-aaea-bf1b7db7f9f3)


Pulsaremos en conectar y seleccionaremos la conexión usb de nuestro ordenador, una vez hecho se nos abrirá la siguiente pestaña:

![image](https://github.com/user-attachments/assets/cf81805a-4e00-4676-83b9-536c14da9371)


Presionaremos en seleccionar archivo, seleccionaremos el archivo .yaml descargado previamente y pulsaremos instalar .

![image](https://github.com/user-attachments/assets/c4a9e80d-d1f4-4666-8de0-20dc7bf553b0)


Una vez hecho todo esto nos iremos al resumen de nuestro **Home Assitant** y veremos que ya nos salen las mediciones de temperatura y humedad.

![image](https://github.com/user-attachments/assets/720f91d8-3cf0-4d2b-b3a5-ce0562331752)

El siguiente sensor sera el de iluminosidad , que seguiremos los mismos pasos que hemos seguido antes con el de humedad pero cambiando algunos detalles.

Una de los apartados que cambian es en nuestra **ESP32** el codigo que tenemos que poner para que el sensor de iluminocidad funcione.
Que sera el siguiente:

![image](https://github.com/user-attachments/assets/667906ea-171a-43dc-a731-82e9decd003c)


Despues de esto lo que tendremos que hacer es la parte de instalar el archivo .yaml como ya hemos explicado antes.
