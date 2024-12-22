# P5 - Montecarlo Laser Localization
In this practice, I implemented the Monte Carlo Localization **(MCL)** algorithm to estimate a robot's pose within a known map using laser sensor data. The algorithm employs a particle filter to maintain multiple pose hypotheses, iteratively refining them based on sensor observations and motion model predictions.

This system enables the robot to navigate a simulated environment while maintaining accurate localization on the map. Notable features include handling noise in both motion and sensor readings, simulating virtual laser measurements for map-based comparisons, and resampling particles to enhance pose estimation accuracy.

## Implementation
For the implementation I followed these steps:
### Particle Initialization:

Particles are uniformly distributed across the map, and their positions are transformed into the world coordinate system using `GUI.mapToPose`.

### Laser Data Processing:
- **Real Laser**: Real laser measurements are read using `HAL.getLaserData()`, and beams are filtered to match the number defined in `LASER_NUM_BEAMS`.
- **Virtual Laser**: Virtual laser beams are generated for each particle using ray tracing with a Digital Differential Analyzer **(DDA)** algorithm.

### Prediction Step:
Particles are propagated based on the robot's odometry data (`HAL.getOdom`), with added noise to account for uncertainty.

### Weight Calculation:
Each particle's weight is computed by comparing its theoretical laser measurements (via ray tracing) with the robot's real laser readings.

Particles outside the map or in obstacle regions are assigned zero weight.

### Resampling:
Particles are resampled using the roulette wheel method, where particles with higher weights have a greater chance of selection.

## Demonstration
Here, I initialize **500 particles** and retain the readings of **10 laser beams** for processing.
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
