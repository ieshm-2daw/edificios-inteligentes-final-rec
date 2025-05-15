## CONFIGURACIÓN DEL MÓDULO RFID MRC522:

En este apartado vamos a instalar y configurar el módulo que vamos a utilizar en nuestra ESP-32, el módulo RFID, más concretamente el modelo MRC522.

El primer paso es conectar físicamente nuestro módulo RFID a nuestra ESP-32. Para ello, deberemos seguir un esquema específico para no provocar errores en el dispositivo o en el módulo. Para conectar nuestro módulo RFID vamos a utilizar una protoboard, aunque hay que tener en cuenta que en algunos dispositivos puede ser necesario soldar los pines a la placa. El esquema que vamos a utilizar para conectar a la ESP-32 es el siguiente:


## Identificación de conectores del sensor:

Para guiarnos sobre dónde tenemos que situar los cables conforme a la dispsición de nuestros conectores, siempre utilizaremos como referencia la siguiente imagen:

<a href="https://github.com/user-attachments/assets/a9237bb0-49b5-4bff-bfff-3a3ab0509a8b">
  <img src="https://github.com/user-attachments/assets/a9237bb0-49b5-4bff-bfff-3a3ab0509a8b" width="300"/>
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

A continuación se muestra cómo quedarían los cables definitivamente:

<a href="https://github.com/user-attachments/assets/c3d0be61-46b2-41c9-9343-b4257bbed3d5">
  <img src="https://github.com/user-attachments/assets/c3d0be61-46b2-41c9-9343-b4257bbed3d5" width="300"/>
</a>


## Configuración en ESPHome:

Una vez que ya tenemos conectado nuestro módulo con nuestra ESP-32 físicamente, pasamos a configurar el sensor para poder realizar acciones con él. Para esto, nos dirigimos a la página prinicpal de Home Assistant y entramos en ESPHome, aquí editaremos nuestro archivo .yaml y añadiremos todo el código necesario para que nuestro módulo sea reconocido por nuestra ESP-32 y sea funcional. En nuestro caso nos hemos remitido a la propia web oficial de Home Assistant, donde nos dan toda la información y código necesarios para la configuración de nuesto módulo (https://esphome.io/components/binary_sensor/rc522.html). Aquí debajo se muestra el código que nos proporciona la propia página, quedando únicamente que cambiar los apartados "_pin:" por los que hemos designado físicamente (posteriormente, una vez que hagamos la primera interacción con los dispositivos nfc que trae el propio módulo, cambiaremos también el apartado "uid:" con el que nos saldrá en los logs).

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

<a href="https://github.com/user-attachments/assets/15eee5e3-2011-4891-abf3-735436dbf00a">
  <img src="https://github.com/user-attachments/assets/15eee5e3-2011-4891-abf3-735436dbf00a" width="300"/>
</a>

<a href="https://github.com/user-attachments/assets/00a51d68-f697-4d23-a7b4-4c67d1463466">
  <img src="https://github.com/user-attachments/assets/00a51d68-f697-4d23-a7b4-4c67d1463466" width="300"/>
</a>

<a href="https://github.com/user-attachments/assets/7eff329c-432f-44d1-8bc4-c4711f4852d2">
  <img src="https://github.com/user-attachments/assets/7eff329c-432f-44d1-8bc4-c4711f4852d2" width="300"/>
</a>


<a href="https://github.com/ieshm-2daw/edificios-inteligentes-final-rec/blob/main/M%C3%B3dulo%20RFID%20MRC522.mp4" target="_blank">Haz click aquí para ir al enlace al video</a>


## Automatización:

Por último he creado una automatización para probar el funcionamiento de nuestro módulo combinado con un relé. La automatización en sí consiste en que si nuestro módulo recibe una lectura del NFC correspondiente, el relé alternará de estado, encendiéndose o apagándose dependiendo del estado original de este.

<a href="https://github.com/user-attachments/assets/b08d7ab9-a350-402d-a224-a0ca86f9395a">
  <img src="https://github.com/user-attachments/assets/b08d7ab9-a350-402d-a224-a0ca86f9395a" width="300"/>
</a>


_Realizado por Alba Martín Díaz_
