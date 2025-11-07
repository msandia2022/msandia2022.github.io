# P3 - Autoparking

## Introducción

En este proyecto he desarrollado un **sistema de aparcamiento autónomo para un coche**. El vehículo detecta la posición de la línea de estacionamiento y busca un hueco libre mediante sensores laser. Una vez identificado, realiza maniobras de avance y retroceso para alinearse correctamente, ajustando su orientación y posición de forma automática.

El sistema se basa en un control por estados donde cada fase del estacionamiento está claramente definida y se ejecuta en función de la información recibida de los sensores y de la posición del coche.

## 1. Aproximación a la línea de estacionamiento

El primer reto fue acercar el coche a la **línea de estacionamiento** de manera precisa. Utilicé los datos del sensor frontal para detectar la proximidad de obstáculos y asegurarme de que el vehículo se encontraba correctamente alineado para iniciar la búsqueda del hueco.

Para controlar la dirección, implementé un **ajuste continuo del ángulo de giro** basándome en la diferencia entre la orientación actual del coche (yaw) y la orientación ideal. Esto permitió mantener una trayectoria recta y evitar oscilaciones al aproximarse a la línea.

## 2. Búsqueda del hueco libre

Una vez alineado con la línea, el coche comenzó a explorar los huecos libres utilizando el sensor lateral derecho. Se definió un rango de ángulos del laser donde la distancia mínima indicaba si había espacio suficiente para estacionar.

Durante esta fase, el coche mantiene una velocidad constante y corrige su orientación para seguir paralelo a la calle, asegurando que el sensor pueda detectar correctamente cualquier hueco disponible.

## 3. Maniobra de estacionamiento

Tras identificar un hueco adecuado, el vehículo realiza la maniobra de aparcamiento en paralelo. Esta consta de varias fases:

- Avance inicial: el coche se coloca frente al hueco.
- Giro hacia atrás (BACK RIGHT): el coche empieza a retroceder girando hacia el interior del hueco.
- Giro contrario (BACK LEFT): cuando se alcanza un ángulo objetivo, el coche corrige la orientación para alinearse completamente dentro del hueco.
- Ajuste final (FORWARD_PARK): el coche avanza ligeramente para quedar completamente dentro del espacio de estacionamiento.

El control de cada fase depende tanto de la posición actual (x) como de la orientación (yaw) del coche, lo que garantiza que se realicen maniobras precisas sin colisiones.

## 4. Control de dirección y velocidad

Para mantener la trayectoria, utilicé un control del giro basado en el error angular con respecto a la orientación deseada. Esto evita movimientos bruscos y asegura una alineación más suave con la línea y con el hueco.

Además, se ajusta la velocidad (V) según la fase: más rápida en desplazamientos libres y más lenta durante los giros para aumentar la precisión de la maniobra.

## 5. Resultados y conclusiones

El coche logró aparcar de forma autónoma y precisa, detectando correctamente los huecos y realizando todas las fases de la maniobra sin intervención externa.

Este proyecto me permitió aplicar conocimientos de control de estados, planificación de maniobras y uso de sensores laser.

Ha sido una práctica muy completa, combinando odometría, programación de sensores y simulación de un entorno real de estacionamiento.

## 6. Video demostrativo

En este vídeo se puede observar el funcionamiento completo del coche durante la maniobra de autoparking con coches en ambos lados:

<video width="600" controls>
  <source src="recursos/aparca_con_coche.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

En este vídeo se puede observar el funcionamiento completo del coche durante la maniobra de autoparking con coches en un lado:

<video width="600" controls>
  <source src="recursos/aparca_sin_coche.mp4" type="video/mp4">
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

