# P2 - Rescue People

## Introducción

En este proyecto he desarrollado un sistema de rescate de víctimas con un dron. Estas son detectadas mediante la cámara y se almacenan sus posiciones para su posterior rescate.
 
## 1. Aproximación a la zona

Para esto fue necesario realizar una transformación de coordenadas. Conocíamos la posición en coordenadas GPS donde se perdió la señal del avión y del barco donde se encuentran el dron y a la vez conociamos la posición del dron en coordenadas del dron. Para solucionarlo transformamos las coordenadas GPS en coordenadas UTM, una vez hecho esto calculabamos la diferencia entre las coordenadas de la zona aproximada de rescate y las del dron. Como el dron se encuentra en la posición (0, 0), obtenemos directamente las coordenadas de zona de rescate en coordenadas del dron. 

## 2. Algoritmo de barrido

Para buscar personas de la forma más minuciosa posible elegí un area concreta, saque todas sus coordenadas e hice que el dron se desplazara por todas ellas siguiendo un patrón de zig zag.

## 3. Detección de caras

A

## 4. Gestión de la batería

Esta funcionalidad la implementé llevando un contador de tiempo, cuando el dron alcanza los 10 minutos de vuelo el dron vuelve a la base para un cambio de batería. A continuación, volverá a despegar para continuar con el barrido por donde iba.

## 5. Visualización y depuración

Durante las pruebas, la **visualización con `WebGUI.showImage()`** fue fundamental.  
Pude observar en tiempo real la detección de las caras.  
Esto me permitió detectar que era necesario rotar la imagen ya que según la posición de la cara esta se detectaba o no.

## 6. Resultados y conclusiones

A

## 7. Video demostrativo

En este vídeo podemos ver al

<video width="600" controls>
  <source src="recursos/rescate.mp4" type="video/mp4">
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

