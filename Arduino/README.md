instrucciones para compilar y ejecutar el código en Arduino:

---

# Proyecto Arduino - Control de Servo con Joystick y Bluetooth

Este proyecto permite controlar dos servomotores para manejar una "grúa" con un joystick y un módulo Bluetooth. Un servomotor se utiliza para el movimiento de un brazo, mientras que el otro permite girar el dispositivo. La comunicación Bluetooth permite realizar ajustes adicionales en la posición del brazo.

## Requisitos

1. **Componentes**:
   - Arduino UNO
   - Dos servomotores
   - Módulo Bluetooth (por ejemplo, HC-05)
   - Joystick (con ejes X e Y)
   - Cables de conexión

2. **Bibliotecas**:
   - `Servo.h`: Biblioteca estándar de Arduino para controlar servomotores.
   - `SoftwareSerial.h`: Biblioteca estándar para comunicación en puertos serie adicionales.

3. **Conexiones**:
   - **Joystick**:
     - Conecta el eje X del joystick al pin `A0` en el Arduino.
     - Conecta el eje Y del joystick al pin `A1` en el Arduino.
   - **Servomotores**:
     - Conecta el primer servomotor al pin digital `9`.
     - Conecta el segundo servomotor al pin digital `10`.
   - **Bluetooth**:
     - RX del módulo Bluetooth al pin `0` (RX) en Arduino.
     - TX del módulo Bluetooth al pin `1` (TX) en Arduino.

## Código

```cpp
#include <Servo.h>
#include <SoftwareSerial.h>

Servo servo1; // Servomotor para el brazo
Servo servo2; // Servomotor para el giro

// Pines para el módulo Bluetooth.
SoftwareSerial bluetooth(0, 1); // RX, TX

int joystickX = A0;
int joystickY = A1;
int valX, valY;

void setup() {
  // Inicia comunicación serial
  Serial.begin(9600);
  bluetooth.begin(9600);
  
  // Configura los pines del joystick como entrada
  pinMode(joystickX, INPUT);
  pinMode(joystickY, INPUT);

  // Asigna los pines a los servos
  servo1.attach(9); 
  servo2.attach(10);
  
  // Posición inicial de los servos
  servo1.write(90);
  servo2.write(90);

  // Delay antes de activar los servomotores
  delay(4000); // Retraso de 2 segundos
}

void loop() {
  // Lee los valores del joystick
  valX = analogRead(joystickX);
  valY = analogRead(joystickY);
  
  // Envio de los valores del joystick a los ángulos del servo (0 a 180 grados)
  int angleX = map(valX, 0, 1023, 0, 180);
  int angleY = map(valY, 0, 1023, 0, 180);

  // Controla los servos con el joystick
  servo1.write(angleX);
  servo2.write(angleY);

  // Control por Bluetooth
  if (bluetooth.available()) {
    char command = bluetooth.read();
    
    switch (command) {
      case 'L': servo2.write(0); break;       // Girar a la izquierda
      case 'R': servo2.write(180); break;     // Girar a la derecha
      case 'U': servo1.write(0); break;       // Subir el brazo
      case 'D': servo1.write(180); break;     // Bajar el brazo
    }
  }

  delay(15); // Pequeña pausa para evitar movimientos bruscos
}
```

## Instrucciones para Compilar y Ejecutar el Código

1. **Abrir el Entorno de Desarrollo de Arduino**:
   - Descarga e instala el [IDE de Arduino](https://www.arduino.cc/en/software) (En caso de no tener el programa).
   - Copia el código en el editor de Arduino.

2. **Conectar el Arduino**:
   - Conecta la placa Arduino a la computadora mediante un cable USB.

3. **Seleccionar la Placa y Puerto**:
   - En el IDE de Arduino, ve a **Herramientas > Placa** y selecciona el modelo de Arduino (en este caso Arduino UNO).
   - Ve a **Herramientas > Puerto** y selecciona el puerto al que está conectado el Arduino.

4. **Compilar y Subir el Código**:
   - Haz clic en el botón **Verificar** (icono de check) para compilar el código y asegurarte de que no haya errores.
   - Luego, haz clic en el botón **Subir** (icono de flecha) para cargar el programa en el Arduino.

5. **Prueba de Funcionamiento**:
   - Una vez cargado el código, utiliza el joystick para mover los servomotores en distintas direcciones.
   - También puedes enviar comandos Bluetooth desde una aplicación de APP INVENTOR (usando las letras `L`, `R`, `U`, y `D` para controlar el giro y el brazo del dispositivo).

## Notas Adicionales

- Asegúrate de que la conexión entre el módulo Bluetooth y el dispositivo que lo controla esté establecida correctamente.
- Ajusta el retardo y las asignaciones de ángulos si necesitas un control de movimiento más preciso o suave.

---


Este README proporciona una descripción del uso del codigo, su contenido y cómo utilizarlo para el dispositivo Arduino. 
