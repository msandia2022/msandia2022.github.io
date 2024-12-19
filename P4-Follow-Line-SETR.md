# P4 - Follow Line

**Authors**: Noelia Casado and Miriam Sandía

In this practice, we have implemented an algorithm that enables a robot to follow a line within a circuit. The robot's behavior is monitored and reported through messages sent using the MQTT protocol. The primary goals are to ensure precise line-following performance and real-time communication of the robot's state.

## Implementation
### Line-Following Algorithm
The line-following algorithm uses data from the robot's infrared sensors to detect the position of the line relative to its trajectory. These sensors are strategically placed on the underside of the robot, enabling it to determine whether the line is in the center, to the left, or to the right. Based on which of the three sensors detects the line, the robot adjusts its movement: it moves straight if the center sensor detects the line, turns left if the left sensor detects it, or turns right if the right sensor detects it.

In situations where none of the sensors detect the line, the robot does not stop immediately. Instead, it uses previously stored information about the last position where the line was detected. Using this memory, the robot continues moving in the corresponding direction, making small adjustments to try to find the line again. This mechanism allows the robot to recover its path even in more challenging sections, such as sharp turns or brief interruptions in the line.

### MQTT Communication
MQTT is used for lightweight and efficient message transmission. The robot publishes its state updates to an MQTT topic.
Each message is formatted in JSON:

**START_LAP**: Notifies the beginning of a lap, signaling the robot is operational and tracking time.

**END_LAP**: Marks the completion of a lap, providing the total time taken.

**OBSTACLE_DETECTED**: Alerts the detection of an obstacle, including the distance to the obstacle.

**LINE_LOST**: Indicates the robot has lost the line and is attempting to recover.

**LINE_FOUND**: Confirms the robot has regained the line after losing it.

**PING**: Periodic "heartbeat" message to confirm the robot's active state and uptime.

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
