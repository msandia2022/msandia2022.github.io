# P1 - Vacuum Cleaner
In this practice, I have implemented a simple algorithm for the navigation of a robot vacuum cleaner using the laser sensors.

## Finite-State Machine
To start developing the algorithm, I defined a list of states and the inputs that trigger the transitions between each state.

1. **`SPIRAL`**: Initially, the robot starts in this state, performing an expanding spiral pattern by keeping a constant angular velocity while gradually increasing its linear velocity with a step factor. Once the linear velocity reaches its max, it transitions to `FORWARD` to explore new open areas. If an obstacle is detected within a threshold, it transitions to `BACKWARD`.

2. **`BACKWARD`**: The robot reverses to safely clear obstacles and avoid getting stuck against walls. Once the path is clear, it transitions to `TURNING`.

3.  **`TURNING`**: The robot rotates on its axis for a non-blocking random duration. This time-based approach introduces the necessary randomness to navigate out of corridors and corners. Upon completion, it transitions to `FORWARD`.

4. **`FORWARD`**: The robot drives straight for a random duration. This long-straight motion allows the robot to travel across room doorways and reach distant areas before initiating a new `SPIRAL`. If an obstacle is detected mid-transit, it immediately switches back to `BACKWARD`.

![FSM Image](rob_mov/FSM.jpg)


## Robot cleaning for 10 minutes
<video width="600" controls>
  <source src="rob_mov/vacuum_cleaner.mp4" type="video/mp4">
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

