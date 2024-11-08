Descripción de la APP y sus instrucciones de uso:

---

# Proyecto ArduinoUno - Aplicación de Control

La aplicación creada en **MIT App Inventor** para controlar un proyecto de Arduino desde un dispositivo móvil. La aplicación permite enviar comandos para controlar direcciones específicas (arriba, abajo, izquierda, derecha), para manejar el movimiento la grúa diseñada en arduino. 

## Carpetas/Contenido del Proyecto

- **Assets**: Contiene imágenes (`up.png`, `down.png`, `left.png`, `right.png`) que se utilizan en la interfaz para indicar los controles de dirección.
- **src/appinventor/ai_tomialvarez78/arduinouno/Screen1.bky**: Contiene los bloques de programación visual que definen la lógica de control y los comandos que se envían desde la aplicación.
- **src/appinventor/ai_tomialvarez78/arduinouno/Screen1.scm**: Define el diseño de la pantalla principal de la aplicación, `Screen1`, incluyendo botones e imágenes de los controles.
- **youngandroidproject/project.properties**: Archivos de configuración y metadatos del proyecto.

## Instrucciones para Importar y Usar la Aplicación

1. **Importar en MIT App Inventor**: 
   - Abre [MIT App Inventor](http://ai2.appinventor.mit.edu/).
   - Selecciona **"Importar proyecto (.aia) desde mi ordenador"** y carga el archivo `arduinouno.aia`.

2. **Ejecutar la Aplicación**:
   - Una vez importado, ejecuta la aplicación en un dispositivo Android. Los botones de dirección enviarán los comandos según la imagen de control que selecciones (arriba, abajo, izquierda o derecha).

3. **Conexión con Arduino**:
   - La aplicación se diseñó para enviar comandos específicos al Arduino a través de un sistema de comunicación vía Bluetooth. Asegúrarse que el dispositivo Android este conectado al modúlo Bluetooth del Arduino y dentro de la aplicacion seleccionar el dispositivo en el apartado de Conectar dispositivo. Luego de hacer los pasos se puede usar se puede utilizar el Arduino.
   
## Uso de los Controles

- **Botones de Dirección**: 
  - Cada botón de la interfaz está enlazado a un comando de dirección (arriba, abajo, izquierda, derecha).
  - Al presionar un botón, la aplicación enviará un comando para que el Arduino realice una acción (por ejemplo, mover un robot en esa dirección).

---
