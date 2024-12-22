# P5 - Montecarlo Laser Localization
In this practice, I implemented the Monte Carlo Localization **(MCL)** algorithm to estimate a robot's pose within a known map using laser sensor data. The algorithm employs a particle filter to maintain multiple pose hypotheses, iteratively refining them based on sensor observations and motion model predictions.

This system enables the robot to navigate a simulated environment while maintaining accurate localization on the map. Notable features include handling noise in both motion and sensor readings, simulating virtual laser measurements for map-based comparisons, and resampling particles to enhance pose estimation accuracy.

## Implementation
### Algorithm Steps
**Particle Initialization**:

Particles are uniformly distributed across the map, and their positions are transformed into the world coordinate system using `GUI.mapToPose`.

**Laser Data Processing**:
- **Real Laser**: Real laser measurements are read using HAL.getLaserData(), and beams are filtered to match the number defined in `LASER_NUM_BEAMS`.
- **Virtual Laser**: Virtual laser beams are generated for each particle using ray tracing with a Digital Differential Analyzer **(DDA)** algorithm.



## Demonstration
<video width="600" controls>
  <source src="recursos/video-P5.mp4" type="video/mp4">
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
