---
title: El desafío de desarrollar con multikinect
category: Personal
---
<br>
Jugadores de Xbox han disfrutado de juegos en los que se controlaba solo con el cuerpo, mientras que los desarrolladores e investigadores han tenido que sufrir para realizar desarrollos en este campo debido a la falta de información.  Hoy os traigo un resumen de  lo que he investigado sobre el desarrollo con Kinect para mi trabajo de final de máster.
<br>
Lo normal es que siendo Xbox de Microsoft solamente se pueda desarrollar bajo entornos Windows pero eso no es del todo cierto, existen librerías como libfreenect que te permiten realizar desarrollos en Linux y Mac, usando el lenguaje de programación C/C++. Pero eso implicaría realizar todo el desarrollo de la interfaz de usuario a mano con librerías como OpenGL, Gtk, Qt y similares.  Si queremos evitar hacerlas, o almenos que el desarrollo sea una semana de desarrollo podemos huir a OpenFrameworks. OpenFrameworks, permite añadir a un proyecto de forma fácil otros componentes como puede ser una librería para Kinect y por defecto trae una librería con la que se puede construir fácilmente la interfaz gráfica.
<br>
Ahora sí, pierdes la capacidad de reconocer el cuerpo del usuario, ya que los desarrollos en OpenFrameworks están basados en la anteriormente mencionada libfreenect la cual no tiene implementado la función del esqueleto.  Si tu Kinect es de Xbox 360, tienes la posibilidad de añadir también los complementos de OpenNI para obtener esta característica.
<br>
Si tu Kinect es del la segunda generación, es decir, de la que viene con la Xbox One, desarrollar se te hace mucho más cuesta arriba. En primer lugar tienes que tener un puerto USB 3.0 donde conectar la Kinect. 
<br>
Si vas a desarrollar en Linux o Mac vas a perder la característica de esqueleto de forma irremediable, puesto que OpenNI dejó de actualizarse en 2012, y la Kinect de Xbox One es de 2014, por lo que los complementos de OpenFrameworks para OpenNI también datan de esa fecha.
<br>
Si solamente vas a tener una cámara Kinect de Xbox One mi recomendación personal es la de desarrollar en Windows, por la de herramientas que te facilitan el trabajo, como el Kinect Studio o Kinect Fusion y todos los ejemplos que te trae el Kinect Browser además del reconocimiento del esqueleto.
<br>
Ahora si tu proyecto tiene dos cámaras Kinect de Xbox One, como es el caso de mi trabajo final de máster, no hay más remedio que usar OpenFrameworks sea cual sea la plataforma si lo que quieres un desarrollo  más rápido, ya que Kinect SDK para Xbox no soporta más de una cámara a la vez y buscarte la vida para detectar el esqueleto.
<br>
También pensé en usar Unity, ya que también es multiplataforma y orientado al desarrollo de videjuego además la interfaz gráfica prácticamente se realiza arrastrando componentes a la escena de desarrollo, pero los complementos de desarrollo en Kinect que hay en la Unity Asset Store son de pago y están construidos sobre el SDK de Microsoft por lo que .
<br>
Espero que este resumen ayude a alguien más que venga con la misma duda. 

**Interesting Links**
- [Kinect SDK 2.0]()https://www.microsoft.com/en-us/download/details.aspx?id=44561
- [Libfreenect](https://github.com/OpenKinect/libfreenect)
- [OpenNI](https://github.com/OpenNI/OpenNI)
- [Kinect v1 Asset for Unity](https://www.assetstore.unity3d.com/en/#!/content/7747)
- [Kinect v2 Asset for Unity](https://www.assetstore.unity3d.com/en/#!/content/18708)
- [OpenFrameworks](http://openframeworks.cc/)
- [Complemento de OpenFrameworks para Kinect v2 - Mac/Linux](https://github.com/ofTheo/ofxKinectV2)
- [Complement de OpenFrameworks para Kinect v2 - Windows](https://github.com/BaptisteTheoriz/ofxKinectV2)