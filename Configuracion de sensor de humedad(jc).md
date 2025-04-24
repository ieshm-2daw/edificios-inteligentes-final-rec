##Instalacion y configuracion del sensor de humedad.

Lo primero que tendremos que hacer sera **conectar el sensor de humedad y temperatura** a nuestra **ESP32** mediante nuestra **protoboard**.

Para ello tendremos que conectar el puerto de 3.3v de nuestra ESP32 a la linea de positivo de nuestra protoboard,lo siguiente sera conectar de nuestra ESP32 el tierra al negativo de nuestra protoboard.El sensor de **humedad** se conectara a nuestra protoboard de la siguiente forma,conectando el pin de **VCC** al 3,3v de nestra protoboard (**el positivo**), el **GND** lo conectaremos al **negativo** y el pin de **DATA** a un puerto cualquiera de nuestra **ESP32** , que no sea ni tierra ni 3,3v.

![IMG20250424105404](https://github.com/user-attachments/assets/9f0f28a1-d377-4959-adff-066f3880555a)


Ahora nos iremos a nuestro HomeAssitant , en el apartado de **ESPHome Builder** y le daremos a edit en nuestra **ESP32**.Una vez dentro tendremos que poner el siguiente codigo:

![image](https://github.com/user-attachments/assets/b5ac3b13-bc34-4227-a64f-7087bf74b86a)

![image](https://github.com/user-attachments/assets/ed6aa6d3-a31a-4096-9ea8-b0c0b231e1c7)


Una vez hecho le daremos a **Save** y a **install**, 
