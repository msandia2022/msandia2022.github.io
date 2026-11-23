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

### 4. Iterative Development and Progress

Before reaching the final line-following architecture:

1. **Initial Approach: 3-Pixel Sampling and HSV Filtering**
   * **Initial design:** To detect the red line quickly, I initially applied a color filter in the full **HSV** color space (filtering H, S, and V channels) and evaluated only **3 specific pixels** at different heights in the image to estimate the track center and compute the lateral error relative to the camera center.
   * **Observed limitations:** This approach proved very fragile on the track. By relying on 3 fixed coordinates, as soon as the car entered a sharp turn, the line shifted outside those sampling points and the vehicle completely lost its reference. Additionally, including the **V (Value)** channel caused track shadows and lighting variations to distort the binary mask, breaking line detection.

2. **Perception Upgrade: Switching to HS Space and Image Moments**
   * **Color space adjustment (HSV to HS):** I removed the strict constraint on brightness (V channel) to focus solely on Hue and Saturation (**HS**), achieving a much more stable segmentation against track shadows and surface glare.
   * **From 3 pixels to global centroid:** I replaced point sampling with **image moments** (`cv2.moments`) computed over the entire segmented Region of Interest (ROI). This calculates the centroid by averaging the entire visible red pixel mass, eliminating point noise and preserving the reference even when the line shifts toward the edges of the frame during tight turns.

3. **Control Stabilization: Dual PID Tuning**
   * With a continuous, jitter-free visual reference, I was able to tune the **two PID controllers** (angular velocity and linear velocity), adjusting their gains to eliminate oscillations on straightaways and automatically reduce speed when approaching high-error curves.

## 5. Circuit Performance & Evaluation
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

