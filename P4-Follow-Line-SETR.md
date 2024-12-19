# P4 - Follow Line

**Authors**: Noelia Casado and Miriam Sandía

In this practice, we have implemented an algorithm that enables a robot to follow a line within a circuit. The robot's behavior is monitored and reported through messages sent using the MQTT protocol. The primary goals are to ensure precise line-following performance and real-time communication of the robot's state.

## Implementation
### Line-Following Algorithm
The line-following algorithm is based on input from the robot's infrared sensor. It detects the position of the line relative to the robot and adjusts its trajectory depending on where it last saw the line.

### MQTT Communication
MQTT is used for lightweight and efficient message transmission. The robot publishes its state updates to an MQTT topic.

## Conclusion
This practice demonstrated the implementation of a line-following robot capable of real-time communication using MQTT. The system achieved reliable line tracking and accurate state reporting.

## Demonstration
<video width="600" controls>
  <source src="recursos/P4-SETR.mp4" type="video/mp4">
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
