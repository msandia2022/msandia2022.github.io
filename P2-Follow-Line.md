# P2 - Follow Line
In this practice, I implemented an algorithm for a self-driving car to follow a red line within a simple circuit. The algorithm processes camera input, detects the line, and adjusts the car's motion using a PID controller.

## Improvements
### HSV Filter
The line detection was enhanced with a more robust HSV filter. The car can now accurately differentiate the red line from other colors, such as white, ensuring reliable navigation on any circuit.

### PID Controller
I upgraded the controller by introducing derivative (D) and integral (I) components to improve stability and accuracy. This refinement reduces oscillations and improves line-following precision.

## Implementation
The algorithm uses the car's camera feed to detect and follow the red line. Below are the main steps:

1. Image Processing:
    The image is converted to HSV color space to isolate red hues using a binary mask.
    A debug image is created to visualize the detected line.

2. Reference Pixels:
    Specific reference points (center, left, and right) are extracted from the image to determine the car's position relative to the line.

3. Position Error Calculation:
    The algorithm computes the error between the expected and actual line position in the image.

4. Control Signals:
    A PID controller calculates the linear and angular velocities based on the position error, ensuring smooth and responsive adjustments.

5. Motion Commands:
    The car moves forward, turns left, or turns right depending on the detected line position.

##  PID controller
The PID controller adjusts the car's motion to minimize the error between the desired path (center of the image) and the actual path:

- Proportional (P): Reacts to the current error.

- Derivative (D): Reduces oscillations by considering the rate of change of the error.

- Integral (I): Addresses accumulated errors over time.

## Car in simple circuit
The car successfully follows the red line in a simple circuit, navigating forward, left, and right turns effectively. The improved HSV filter ensures robust line detection, and the PID controller enhances stability and responsiveness. The circuit is completed in 94 seconds.

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

