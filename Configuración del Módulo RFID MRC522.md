## CONFIGURACIÓN DEL MÓDULO RFID MRC522:

En este apartado vamos a instalar y configurar el módulo que vamos a utilizar en nuestra ESP-32, el módulo RFID, más concretamente el modelo MRC522.

El primer paso es conectar físicamente nuestro módulo RFID a nuestra ESP-32. Para ello, deberemos seguir un esquema específico para no provocar errores en el dispositivo o en el módulo. Para conectar nuestro módulo RFID vamos a utilizar una protoboard, aunque hay que tener en cuenta que en algunos dispositivos puede ser necesario soldar los pines a la placa. El esquema que vamos a utilizar para conectar a la ESP-32 es el siguiente:


## Identificación de conectores del sensor:

- Color Blanco: Este cable está conectado al puerto SDA del módulo, que en nuestro ESP-32 corresponde al pin D5 (GPIO5). Este cable es responsable de la transmisión de datos en protocolos de comunicación como I2C, por lo que es fundamental asegurarse de que esté bien conectado para garantizar una correcta comunicación entre el módulo y la placa.

- Color Naranja: Este cable corresponde al pin SCK del módulo, y en nuestra ESP-32 lo hemos conectado al pin D18 (GPIO18). El pin SCK (Serial Clock) se encarga de sincronizar la comunicación SPI entre dispositivos, actuando como señal de reloj.

- Color Amarillo: Este cable conectado al puerto MOSI del módulo y al pin D23 (GPIO23) de nuestra ESP-32.
MOSI (Master Out Slave In) es el canal por el cual el microcontrolador (ESP-32) envía datos hacia el módulo. Es crucial que este cable esté correctamente conectado para asegurar que el módulo reciba las instrucciones adecuadas.

- Color Azul: Este cable se conecta al pin MISO del módulo y al pin D19 (GPIO19) de la ESP-32. MISO (Master In Slave Out) es el canal por el cual el módulo devuelve información al microcontrolador. Sin este cable, no podríamos recibir datos desde el módulo.

- Color Negro: Este cable se encuentra conectado al pin GND del módulo, y va también al puerto GNID de nuestra ESP-32. Es fundamental realizar esta conexión en primer lugar para establecer una referencia común de voltaje y evitar posibles daños por diferencias de potencial.

- Color Rojo: Este cable alimenta el módulo con energía eléctrica. En este caso, lo hemos conectado al pin de 3.3V de la ESP-32, ya que el módulo está diseñado para trabajar con este voltaje. Conectarlo a un voltaje superior podría dañar permanentemente el módulo.

<div align="center">
  
| Colores | Negro | Blanco | Naranja | Amarillo | Azul | Rojo |
|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|
| Puerto del Módulo | GND | SDA | SCK | MOSI | MISO | 3.3V |
| ESP32 | GND | D5 | D18 | D23 | D19 | 3V |

</div>
