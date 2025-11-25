# P4 - Robot de almacén

## Introducción

En este proyecto he desarrollado un **robot autónomo de almacén** capaz de desplazarse por un entorno cargado de obstáculos, recoger estanterías y devolverlas a la base siguiendo trayectorias seguras y eficientes. El sistema combina planificación de rutas con el planificador **RRT\***, control de movimiento con *Pure Pursuit* y un ciclo de estados que guía todas las fases de trabajo: aproximación, carga, retorno y descarga.

Un aspecto importante del proyecto es el uso de dos modelos de movimiento distintos según el tipo de robot:  
- En **modo holonómico**, el sistema utiliza `SE2StateSpace`, lo que permite planificar movimientos libres en el plano sin restricciones de giro.  
- En **modo Ackermann**, el robot emplea `ReedsSheppStateSpace`, adecuado para robots con restricciones de radio de giro y que pueden avanzar tanto hacia adelante como hacia atrás.

Esta diferenciación permite que el mismo planificador se adapte a distintos comportamientos cinemáticos según las necesidades del entorno o del robot.

## 1. Aproximación a la estantería objetivo

El robot inicia su ciclo seleccionando una de las estanterías marcadas como objetivo. Utiliza su pose actual para calcular una trayectoria hacia la estantería, transformando coordenadas del mundo al mapa y planificando una ruta con RRT\*.  

La elección del espacio de estados depende del modo de movimiento:  
- En **holonómico**, el planificador usa `SE2StateSpace`, lo que le permite generar trayectorias suaves sin preocuparse por limitaciones de giro.  
- En **Ackermann**, se emplea `ReedsSheppStateSpace`, generando rutas viables para vehículos con geometría de coche, respetando su radio de giro.

Durante esta fase, el objetivo es **llegar al estante sin colisionar**, ajustando el movimiento según la geometría del almacén. El control Pure Pursuit mantiene el robot estable y dirige suavemente el giro, evitando oscilaciones incluso en pasillos estrechos.

## 2. Carga de la estantería

Una vez alcanzada la posición objetivo, el robot detiene la navegación y activa el mecanismo de elevación. Esta fase consiste en **levantar la estantería**, asegurando que queda acoplada al robot para su transporte.

Tras la elevación, el sistema realiza un paso muy importante: **actualiza el mapa eliminando la estantería levantada**, de forma que la planificación de la trayectoria de vuelta no la considere un obstáculo.

## 3. Retorno a la base

Con la estantería ya cargada, el robot calcula una nueva ruta, esta vez de vuelta a la base. El mapa actualizado permite que el planificador encuentre un camino completamente libre, evitando el lugar donde antes estaba la estantería.

De nuevo, el espacio de estados elegido depende del modo del robot:  
- En modo holonómico, `SE2StateSpace` ofrece libertad total para generar rutas limpias.  
- En modo Ackermann, `ReedsSheppStateSpace` garantiza que la trayectoria sea físicamente ejecutable, permitiendo maniobras hacia adelante y hacia atrás.

El robot avanza punto por punto siguiendo la nueva trayectoria. El controlador ajusta la velocidad, el giro y detecta si es necesario avanzar marcha atrás, siempre priorizando trayectorias suaves y seguras.

## 4. Descarga y preparación para la siguiente estantería

Cuando llega a la base, el robot baja la estantería, libera la carga y realiza una pausa breve. En este momento el sistema actualiza su estado interno para seleccionar la siguiente estantería que debe recoger.

Si aún quedan estanterías por transportar, el robot reinicia el ciclo de navegación. En caso contrario, finaliza su operación y se detiene de forma segura.

## 5. Funcionamiento de Pure Pursuit

El control **Pure Pursuit** es una técnica muy utilizada en robots móviles para seguir trayectorias suaves sin necesidad de cálculos complejos. La idea es sencilla: en lugar de corregir constantemente el error respecto a la línea ideal del camino, el robot selecciona un punto adelantado de la trayectoria —el *lookahead*— y calcula el arco con el que debería girar para dirigirse hacia él. Si el punto está centrado, avanza recto; si está a un lado, gira con la curvatura necesaria para reencontrar la ruta. Este método genera movimientos estables y fluidos, lo que lo hace especialmente adecuado para entornos estrechos como un almacén.

## 6. Resultados y conclusiones

El robot logró desplazarse con éxito por el almacén, planificar rutas entre obstáculos y transportar estanterías sin colisiones. Gracias al uso combinado de planificación RRT\*, validación geométrica, control Pure Pursuit y un ciclo de estados bien estructurado, el comportamiento se mantuvo estable y autónomo en todo momento.

Además, la posibilidad de alternar entre `SE2StateSpace` y `ReedsSheppStateSpace` permite adaptar el robot tanto a movimientos completamente libres como a movimientos con restricciones tipo vehículo, ampliando la flexibilidad del sistema.


## 7. Funcionamiento en vídeo

En este vídeo se puede observar el ciclo completo del robot holonómico: planificación hacia la estantería, elevación, retorno a la base, descarga y repetición del procedimiento con la segunda estantería.

<video width="600" controls>
  <source src="recursos/robot_almacen_hol.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

En este vídeo se puede observar el ciclo del robot Ackermann.

<video width="600" controls>
  <source src="recursos/robot_almacen_ack.mp4" type="video/mp4">
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

