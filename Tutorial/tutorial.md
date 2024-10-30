Materiales Necesarios:
Hardware:
        ◦ Arduino Uno o compatible
        ◦ 2 Servomotores (SG90 o similares)
        ◦ Módulo Bluetooth HC-05 o HC-06
        ◦ Joystick (con módulo)
        ◦ Protoboard y cables de conexión
        ◦ Fuente de alimentación (baterías o adaptador)
        ◦ Estructura de la grúa (se puede hacer con materiales como cartón, madera, etc)
Software:
        ◦ Arduino IDE
        ◦ App Inventor (para crear la app de control)
​Paso 1: Montaje del Hardware
Estructura de la Grúa:
        ◦ Construye la estructura de la grúa utilizando los materiales que has elegido. Asegúrate de que los servomotores estén bien fijados para que el movimiento sea fluido.
Conexiones de los Servomotores:
        ◦ Conecta el primer servomotor (Brazo) al pin 9 del Arduino.
        ◦ Conecta el segundo servomotor (Giro) al pin 10 del Arduino.
        ◦ Conecta los cables de alimentación (VCC y GND) de ambos servomotores a la fuente de alimentación.
Conexiones del Módulo Bluetooth:
        ◦ Conecta el pin VCC del HC-05 a 5V del Arduino.
        ◦ Conecta el pin GND del HC-05 a GND del Arduino.
        ◦ Conecta el pin TX del HC-05 al pin RX (0) del Arduino.
        ◦ Conecta el pin RX del HC-05 al pin TX (1) del Arduino.
Conexiones del Joystick:
        ◦ Conecta el pin VCC del joystick a 5V.
        ◦ Conecta el pin GND del joystick a GND.
        ◦ Conecta el pin de salida X a un pin analógico (A0).
        ◦ Conecta el pin de salida Y a otro pin analógico (A1).

​Paso 2: Código en Arduino
Abre el Arduino IDE y carga el siguiente código:
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
}

void loop() {
// Lee los valores del joystick
valX = analogRead(joystickX);
valY = analogRead(joystickY);
// Mapeo de los valores del joystick a los ángulos del servo (0 a 180 grados)
int angleX = map(valX, 0, 1023, 0, 180);
int angleY = map(valY, 0, 1023, 0, 180);

// Controla los servos con el joystick
servo1.write(angleX);
servo2.write(angleY);

// Control por Bluetooth
if (bluetooth.available()) {
char command = bluetooth.read();
switch (command) {
case 'L': servo2.write(0); break; // Girar a la izquierda
case 'R': servo2.write(180); break; // Girar a la derecha
case 'U': servo1.write(0); break; // Subir el brazo
case 'D': servo1.write(180); break; // Bajar el brazo
}
}

delay(15); // Pequeña pausa para evitar movimientos bruscos
}

Paso 3: Crear la App en App Inventor

Accede a App Inventor:
        ◦ Ve a App Inventor y crea un nuevo proyecto.
Diseña la Interfaz:
        ◦ Agrega 4 botones para mover la Grua.
        ◦ Agrega un ListPicker para conectar el Bluetooth.
        ◦ Agrega un componente BluetoothClient.
Programar la Lógica:
        ◦ Programa el ListPicker para que busque y se conecte al dispositivo Bluetooth.
        ◦ Envía los valores de los botones al Arduino a través del Bluetooth.

Paso 4: Prueba y Ajustes
Carga el Código en Arduino:
        ◦ Conecta tu Arduino a la computadora y carga el código.
Prueba la App:
        ◦ Abre la app en tu celular móvil, conéctate al módulo Bluetooth y utiliza los botones para controlar la grúa.

Conclusion: 
¡Felicitaciones! Has construido con éxito un proyecto de grúa controlada por Bluetooth con Arduino.
