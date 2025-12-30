# P6 - Localización Visual mediante AprilTags

## Introducción

En este proyecto he implementado un sistema de **localización** para un robot móvil utilizando visión y odometría incremental. El objetivo principal es que el robot sea capaz de estimar su posición global en un mapa mediante la detección de balizas visuales (**AprilTags**) y mantener dicha estimación de forma precisa incluso cuando no tiene ninguna baliza a la vista (navegación "a ciegas").

## 1. Detección de Balizas (AprilTags)

El primer paso fue integrar un sistema de visión capaz de identificar las balizas en el entorno. Utilicé la librería `pyapriltags` para detectar los tags en la imagen capturada por la cámara del robot. 

Para optimizar la precisión, implementé una lógica que selecciona únicamente la **baliza más cercana** (`closest_tag`) en cada frame. Esto es fundamental porque las detecciones lejanas suelen introducir más ruido en el cálculo de la distancia y la orientación.

## 2. Resolución de la Pose (PnP)

Para determinar la posición del robot respecto a la baliza, utilicé el algoritmo **SolvePnP** de OpenCV. 
- Definí los puntos 3D de la baliza (`object_points`) basados en su tamaño real de 30 cm.
- Obtuve los vectores de rotación (`r_vec`) y traslación (`t_vec`) que sitúan la baliza respecto a la cámara.
- Implementé una función de calibración dinámica (`get_camera_params`) que genera la matriz intrínseca basándose en las dimensiones de la imagen, permitiendo que el sistema sea flexible a cambios de resolución.



## 3. Localización Global mediante Transformadas

Una vez obtenida la posición relativa (Robot -> Baliza), el desafío fue convertirla en una **posición global (Mundo -> Robot)** utilizando un archivo de configuración YAML con las coordenadas reales de cada tag.

Implementé un proceso de transformación matemática en dos pasos:
1. **Inversión**: Transformé la rotación y traslación para obtener la posición de la cámara respecto al tag (invirtiendo la matriz de rotación mediante su transpuesta).
2. **Proyección**: Utilizando el `yaw` absoluto de la baliza en el mapa, roté la distancia relativa calculada y la sumé a las coordenadas de la baliza.

Esto permite que, cada vez que el robot ve una baliza, su posición se "resetee" a la posición real, eliminando instantáneamente cualquier error acumulado por el movimiento.

## 4. Odometría Incremental

El robot no siempre tiene balizas a la vista. Para solucionar esto, implementé un sistema de **fallback basado en odometría incremental**. 

Cuando no hay tags detectados, el robot mide el incremento de movimiento (`dx`, `dy`, `dyaw`) proporcionado por sus sensores internos entre cada iteración. Este "delta" se proyecta utilizando el ángulo estimado actual (`est_yaw`). Este método permite al robot mantener una estimación coherente de su trayectoria hasta que encuentra la siguiente baliza para corregirse.

## 5. Navegación y Evasión de Obstáculos

Para que el robot explore el entorno de forma autónoma, integré un algoritmo de navegación reactiva basado en sensores **Láser**. 

El robot analiza los datos del láser dividiéndolos en tres sectores principales:
- **Frontal**: Si el camino está despejado, el robot avanza a velocidad constante.
- **Lateral (Izquierda/Derecha)**: Si detecta proximidad a una pared, aplica una velocidad angular para alejarse.
- **Evasión Crítica**: Si el obstáculo es frontal y cercano, el robot se detiene y gira sobre su propio eje hacia el lado con más espacio.

## 6. Visualización y Depuración

Durante el desarrollo, la depuración visual fue clave. Utilicé las herramientas de la plataforma para superponer información:
- **Bounding box**: Dibujado sobre cada AprilTag detectado.
- **Ejes 3D**: Proyectados sobre la baliza para verificar que el algoritmo PnP calculaba correctamente la orientación.
- **Pose Estimada**: Representada en el mapa global para observar en tiempo real cómo la odometría "deriva" y cómo la visión "corrige" la posición.

## 7. Resultados y Conclusiones

El sistema logra una navegación fluida y una localización aproximada. La visión nos da la "verdad absoluta" del mapa, mientras que la odometría nos da la "continuidad" necesaria para no perdernos entre baliza y baliza.

## 8. Video demostrativo

En el siguiente video se observa al robot navegando por el entorno. Se puede apreciar cómo el sistema detecta los tags, dibuja los ejes de coordenadas y mantiene la localización estimada incluso en los tramos donde navega solo por odometría.

<video width="600" controls>
  <source src="recursos/visual_markers_1.mp4" type="video/mp4">
  Tu navegador no soporta videos.
</video>

<video width="600" controls>
  <source src="recursos/visual_markers_2.mp4" type="video/mp4">
  Tu navegador no soporta videos.
</video>

<style>
  body {
    background-color: #121212;
    color: #E0E0E0;
  }

  h1, h2, h3 {
    color: #BB86FC;
  }

  a {
    color: #03DAC6;
  }

  video {
    border: 2px solid #BB86FC;
  }
</style>
