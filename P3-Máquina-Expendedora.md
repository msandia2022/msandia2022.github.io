# P3 - Máquina Expendedora
Este proyecto tiene como objetivo el desarrollo de una máquina expendedora automatizada que combina diferentes tecnologías para ofrecer una experiencia interactiva y eficiente. A continuación, se detallan las funcionalidades, componentes, estructura del sistema y otros aspectos clave del proyecto.

## Funcionalidades del Sistema
### Arranque y Servicio
La máquina expendedora inicia su funcionamiento con una animación en la pantalla LCD, acompañada de un LED que indica que el sistema está cargando. A continuación, la máquina comienza a detectar la presencia de un cliente mediante un sensor ultrasónico. Cuando se detecta la presencia de un cliente, la máquina muestra la temperatura y la humedad ambiente en la pantalla LCD. El usuario puede navegar por las opciones de bebidas utilizando un joystick, lo que permite seleccionar entre las bebidas disponibles. Una vez seleccionada la bebida, el sistema comienza el proceso de preparación, indicado por el parpadeo del LED. Cuando la bebida está lista, la máquina muestra un mensaje en la pantalla LCD indicando que el usuario puede retirar la bebida.

### Modo Administrativo
El sistema también cuenta con un modo administrativo, accesible mediante una pulsación prolongada del pulsador. En este modo, el administrador tiene acceso a diferentes opciones, como la visualización de la temperatura y la distancia medida por el sensor ultrasónico, la modificación de los precios de las bebidas y la monitorización del tiempo total de ejecución del sistema.

## Estructura y Flujo del Sistema
### Estados Principales
El sistema se organiza en diferentes estados que controlan el flujo de las acciones. Cada estado se corresponde con una fase específica del servicio que ofrece la máquina expendedora. Los estados principales incluyen el arranque del sistema, la espera del cliente, la visualización de la temperatura y humedad, la selección de la bebida, la preparación de la bebida, la entrega de la bebida y el reinicio del servicio para un nuevo ciclo. Estos estados permiten que el sistema pase de una fase a otra de forma ordenada y eficiente.

### Transición entre Estados
El sistema transita de un estado a otro según las interacciones del usuario y las condiciones del sistema. Por ejemplo, la máquina pasa del estado de "Esperando Cliente" al estado de "Mostrar Bebidas Disponibles" una vez que se detecta la presencia de un cliente. Igualmente, tras la preparación de la bebida, la máquina cambia al estado de "Retirar Bebida", donde el usuario puede recoger su pedido.

## Tareas Concurrentes
El sistema está diseñado para ejecutar varias tareas de forma simultánea utilizando hilos. Esto permite que el sistema realice diferentes acciones sin bloqueos, mejorando la eficiencia y la interacción con el usuario. Entre las tareas concurrentes, se incluyen el control de los LEDs, la actualización de la pantalla LCD, la detección de clientes y la monitorización de la temperatura y humedad. Cada una de estas tareas se maneja mediante hilos independientes, lo que optimiza el rendimiento general del sistema.

## Watchdog Timer (WDT)
El Watchdog Timer (habilitado con wdt_enable(WDTO_2S)) garantiza la recuperación automática en caso de fallos del sistema, como bloqueos o loops infinitos. Esto añade robustez al sistema, ya que si el programa no llama a wdt_reset() dentro de 2 segundos, el microcontrolador se reinicia automáticamente, asegurando la continuidad del servicio.

## Componentes Utilizados
### Sensores y Dispositivos
El sistema utiliza una serie de sensores y dispositivos para interactuar con los usuarios y ofrecer información relevante. Los principales componentes son:

- Pantalla LCD: Muestra información importante al usuario, como las opciones de bebidas, las condiciones ambientales y los mensajes del sistema.
- Sensor ultrasónico: Detecta la presencia de un cliente, lo que permite activar el proceso de selección de bebidas.
- Sensor de temperatura y humedad (DHT11): Mide las condiciones ambientales y las muestra en la pantalla LCD.
- Joystick: Permite al usuario interactuar con la máquina para seleccionar bebidas y navegar por el menú administrativo.
- LEDs: Indicadores visuales que muestran el estado del sistema, como el progreso de la preparación de la bebida y el estado general de la máquina.

## Innovaciones y Ventajas
### Interfaz de Usuario Intuitiva
El uso del joystick y la pantalla LCD permite que la máquina tenga una interfaz de usuario fácil de usar. La navegación por el menú de bebidas y las opciones de administración es sencilla y accesible para los usuarios.

### Modularidad y Escalabilidad
El sistema está diseñado para ser modular, lo que significa que es fácil añadir nuevas funcionalidades o modificar las existentes. El uso de hilos para gestionar tareas concurrentes asegura que el sistema pueda manejar múltiples procesos al mismo tiempo sin problemas de rendimiento.

### Monitorización y Personalización
Los sensores proporcionan información valiosa sobre las condiciones ambientales, lo que permite ofrecer un servicio más personalizado. Además, el modo administrativo ofrece al administrador la capacidad de modificar los precios de las bebidas y monitorizar el rendimiento del sistema.

## Conclusión
Este proyecto de máquina expendedora automatizada combina hardware y software de manera efectiva, creando una solución que no solo proporciona un servicio rápido y eficiente, sino que también permite una interacción sencilla y personalizable tanto para los usuarios como para los administradores. Gracias a la integración de sensores, controles de precios y un sistema basado en hilos, el sistema es robusto, escalable y flexible.

## Esquema de conexión

## Demostración
<video width="600" controls>
  <source src="recursos/video-maquina-exp.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<style>
  body {
   background-color: #121212; /* Fondo oscuro */
    color: #E0E0E0; /* Texto claro */
  }

  h1, h2, h3 {
    color: #BB86FC; /* Púrpura para encabezados */
  }

  a {
    color: #03DAC6; /* Verde azulado para enlaces */
  }

  video {
    border: 2px solid #BB86FC; /* Borde púrpura alrededor del video */
  }
</style>
