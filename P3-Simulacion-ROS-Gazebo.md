# P3 - Simulación en ROS y Gazebo
    
## TIEMPO VS G-PARCIAL
Explicación detallada de las gráficas generadas, describiendo el comportamiento del robot en momentos específicos durante la teleoperación.


<img src="/recursos/efforts_sombreado.png" width="900">

<img src="recursos/gif_efforts.gif" width="900">




## TIEMPO VS POSICIÓN DE LAS RUEDAS

<img src="/recursos/apartado5.png" width="900">

Esta gráfica muestra la evolución de la posición de las ruedas del rover, lo que permite analizar cómo se ha desplazado para asistir al brazo robótico.

Al inicio, podemos observar un aumento rápido y simultáneo de todas las ruedas, indica que el rover comienza a moverse con trayectoria recta.

A la mitad, hay variaciones desiguales entre las ruedas delanteras y traseras, lo que reflejan las maniobras de reposicionamiento para recoger el cubo correctamente.

Al final, las ruedas se mantienen constantes, esto se debe a que el rover se mantiene estacionario mientras se ejecuta el pick and place.

<img src="recursos/gif_pos.gif" width="900">

## ACCESO A ROSBAG
Enlace a rosbag en GitHub:

📦 [rosbag](https://github.com/msandia2022/msandia2022.github.io/tree/main/recursos/rosbag2_2025_05_10-20_23_55)


## VÍDEO EJECUCIÓN
<video width="600" controls>
  <source src="recursos/Ejecución_rover.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## GALERÍA

<img src="recursos/apartado3.png" width="900">

<img src="recursos/Captura desde 2025-05-10 20-29-24.png" width="900">

<img src="recursos/apartado2.png" width="900">

<img src="recursos/Captura desde 2025-05-10 15-20-12.png" width="900">





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
