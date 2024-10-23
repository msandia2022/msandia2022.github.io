# P3 - Obstacle Avoidance
In this practice, I implemented an algorithm for a self-driving car to navigate towards waypoints while avoiding obstacles using the Virtual Force Field (VFF) Algorithm. The goal is to balance the attractive force pulling the robot towards its target with the repulsive forces pushing it away from nearby obstacles.

## Implementation
### Forces Calculation
- Attractive Force: The robot calculates a vector pointing towards the target, with a magnitude scaled by the constant ALPHA. This force pulls the robot towards the goal.

- Repulsive Force: The robot computes repulsive forces from obstacles detected by the laser scanner. Each laser point creates a repulsive vector inversely proportional to the square of the distance to the obstacle, scaled by BETA.

### Resultant Force and Movement
The total force is the sum of the attractive and repulsive forces. The robot adjusts its velocity based on the direction of this resultant force:
- Angular Velocity (W): Determines how much the robot should turn towards the resultant force direction.

- Linear Velocity (V): Calculated based on the angular velocity, making the robot slow down as it turns sharply.

## Demonstration
<video width="600" controls>
  <source src="recursos/video-P3.mp4" type="video/mp4">
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
