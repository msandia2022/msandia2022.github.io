# P2 - Follow Line
In this practice, I implemented an algorithm for a self-driving car to follow a red line across different circuits. The algorithm processes camera input, detects the line, and adjusts the linear and angular velocities using dual PID controllers.

## Implementation
### 1. Color Segmentation Strategy (HS Filtering)
To make the vision robust against changing lighting conditions, shadows, and track reflections, I transitioned from a basic RGB thresholding to a specialized **Hue-Saturation (HS) filter**. 
- **Hue Isolation:** Red wraps around both ends of the color spectrum, so two distinct hue sub-ranges were merged to capture all shade variations accurately.
- **Ignoring Brightness (Value):** The Value (V) channel limits were set to cover the full spectrum. By relying solely on Hue and Saturation, the car remains unaffected by shadows or bright highlights on the track.

### 2. Centroid Tracking via Image Moments
Instead of sampling static reference pixels across fixed lines, I implemented a dynamic **Region of Interest (ROI)** combined with **Image Moments**.
- The algorithm focuses on a target horizontal band ahead of the car to compute the geometric center (centroid) of the detected line mass.
- This provides a smooth, continuous positional metric relative to the frame center.
- **Fail-safe Logic:** If the line is temporarily obscured or lost during extreme turns, the system retains the previous valid positional feedback to prevent sudden erratic steering.

### 3. Dual PID Controller Architecture
Rather than relying on fixed forward speeds or simple proportional steering, I built two complementary closed-loop controllers:

- **Steering Control (Angular Velocity):** 
  - **Proportional:** Corrects immediate lateral displacement from the line center.
  - **Integral:** Compensates for systematic drift, with anti-windup bounds to prevent overshoot.
  - **Derivative:** Dampens rapid oscillations when crossing or re-entering the line alignment.
  
- **Adaptive Speed Control (Linear Velocity):**
  - Evaluates the magnitude of the positioning error in real time.
  - Automatically modulates speed: maximum velocity on straightaways, smoothly slowing down when entering tight corners or sharp bends.


## Circuit Performance & Evaluation
The car successfully follows the red line in every circuit, navigating forward, left, and right turns effectively. The improved HS filter ensures robust line detection, and the dual PID controllers enhance stability and responsiveness. The simple circuit is completed in 48 seconds.

### Simple Circuit
<video width="600" controls>
  <source src="rob_mov/def_circ_simple.webm" type="video/webm">
  Your browser does not support the video tag.
</video>

### Montmeló Circuit
<video width="600" controls>
  <source src="rob_mov/def_circ_montmelo.webm" type="video/webm">
  Your browser does not support the video tag.
</video>

### Montreal Circuit
<video width="600" controls>
  <source src="rob_mov/def_circ_montreal.webm" type="video/webm">
  Your browser does not support the video tag.
</video>

### Nürburgring Circuit
<video width="600" controls>
  <source src="rob_mov/def_circ_nurburgring.webm" type="video/webm">
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

