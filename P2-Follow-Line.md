# P2 - Follow Line
In this practice, I implemented an algorithm for a self-driving car to follow a line within a simple circuit.

## Mejoras
HSV FILTER: Ahora el coche puede circular perfectamente en cualquier circuito, ya no confunde lineas blancas con lineas rojas.


## Implementation
To develop the algorithm, I used the image from the car's camera to follow the line.

First, I processed the image and applied color filtering to detect only the red line on the road.

Next, I selected specific pixels to track the line and determine the car’s position relative to it.

Based on this, I defined several conditions to steer the car accordingly.

##  PD controller
To fine-tune the car's velocities, I implemented a PD controller that reacts to the distance between the line and the center of the image. In other words, the velocities are adjusted based on the difference between the car's desired path and its actual path (the error).

The derivative part of the controller (D) was intended to reduce oscillations, but I couldn’t find an optimal value for it :(.

## Car in simple circuit
<video width="600" controls>
  <source src="recursos/video-P2.mp4" type="video/mp4">
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

