# GravityMaze

<h1>Descarga</h1>
El proyecto con todos sus assets se puede descargar <a href=https://drive.google.com/file/d/1ye5muySIwuZo02_79GXE9KQx_9IAY_ga/view?usp=sharing>aquí</a>.

<h2>Gameplays</h2>
Algunos gameplays ganando y perdiendo se pueden encontrar <a href=https://drive.google.com/drive/folders/1SYcLSYliSC_zIPB0aSiY3i3J2sXYGzQb?usp=sharing>aquí</a>.

<h1>Requerimientos</h1>

<ul>
  <li>Insatalar <code>ProBuilder</code>.</li>
  <li>Configurar <code>New input system</code>.</li>
  <li>Importar paquete <code>Battle Wizard Poly Art</code> del asset store.</li>
  <li>Importar paquete <code>Little Ghost lowpoly(FREE)</code> del asset store.</li>
  <li>Importar paquete <code>Cinemachine</code> del asset store.</li>
  <li>Importar paquete <code>AllSky Free - 10 Sky / Skybox Set</code> del asset store.</li>
</ul>


<h2>Contexto</h2>

<p>Este juego es inspirado en <code>Portal</code>. Tomamos como inspiración un <code>Shooter puzzle game</code>, donde nuestro objetivo no es matar nada sino resolver un acertijo para poder continuar. Para el <code>Final boss</code> nos inspiramos directamente del final boss de portal 1 <code>GLaDOS</code> y en el final boss de portal 2 <code>Wheatly</code>.</p>


<h2>Primeros pasos</h2>

<p>Una vez instalamos <code>ProBuilder</code>, creamos un plano, este será nuestro primer escenario en donde estaremos trabajando todas las mecánicas del jugador para luego crear los escenarios de juego detalladamente.</p>


<image
  src="GravityMaze/firstMaze.png"
  width = 60%
  height = 60%>


<h2>Manejo de input y animaciones</h2>

<p> Previamente configuramos el movimiento de nuestro jugador utilzando el <code>New Input System</code>. Con esto hecho, uno de los primeros retos que decidimos enfrentar fue manejar que cada animación se presentara en el momento adecuado. Para esto básicamente generamos una máquina de estados finitos creando dentro de un <code>Animation controller</code>.</p>


<image
  src="GravityMaze/animaciones.gif"
  width = 60%
  height = 60%>


<h2>Bala que rebota las paredes.</h2>

<p>Otro de los factores que el jugador debe tener en cuenta es que si una de sus balas choca una pared la bala rebotará y le afectará bajandole la velocidad en 0.20 por cada bala. OJO, puede llegar a valores negativos también, pero con un límite. </p>

<image
  src="GravityMaze/balaRebota.gif"
  width = 60%
  height = 60%>

  <p>Este es el código asociado a que la bala rebote. Las paredes tienen un script llamado "life" y se hacen algunas validaciones cuando la bala hace contacto.</p>

<image
  src="GravityMaze/balaRebotaCode.png"
  width = 60%
  height = 60%>



<h2>Dinámica de disparo y cumplir objetivo.</h2>

<p>Durante este juego el objetivo es poder encontrar el camino que culmine el laberinto. Durante la fase 1 queremos mantener la dinámica sencilla para que el jugador se familiarice con el movimiento, disparo y dinámica. Primero aparecerá en el laberinto con lo que es por ahora un cubo en frente. Este cubo tendrá otro encima, fuera del alcanze de las balas del jugador. La idea de este segundo cubo es que funcione como un botón, que al chocar, instancíe el próximo cubo que estará debajo del próximo botón. Una vez sea el último botón de la saga de botones, entonces se destruirá la pared que esté asociada al mismo. </p>



<image
  src="GravityMaze/cubeButton.png"
  width = 60%
  height = 60%>



<h2>Gameplay de la primera fase como un tutorial.</h2>

<p>En este gameplay se puede ver como al principio aparece un cubo enfrente con un cubo arriba. El player dispara al cubo lo que le cambia su gravedad y ace que el cubo suba y choque el cubo de arriba. Una vez el botón de arriba es activado el próximo cubo se instancia al que se puede hacer lo mismo que el anterior. Como este botón es el último, se destruye la pared que bloqueaba el paso.</p>


<p>En esta imagen puede ver un esquema de lo que es la fase 1. El area de los arboles es donde sucede la teletransportación a la próxima fase.</p>
<image
  src="GravityMaze/esquema.png"
  width = 60%
  height = 60%>

<image
  src="gameplay1.gif"
  width = 60%
  height = 60%>



<p>Para hacerlo mas adecuado al ambiente decidimos que en vez de cubos usaremos troncos, que el usuario puede disparar y cambiarle su gravedad.</p>
  <image
  src="imagen.png"
  width = 60%
  height = 60%>


<h2>Cómo se conoce donde se debe instanciar el próximo cubo?</h2>

<p>Los objetos tipo "cubo" tienen asociados un script que solo detecta si hubo un collider de parte de la bala del player y le "cambia" la gravedad. En la práctica solo le aumenta la velocidad en dirección hacia arriba. Cuando choca con un botón deja de subir. </p>

<image
  src="GravityMaze/cube.png"
  width = 60%
  height = 60%>


  <p>Una vez se choca con este botón, se instancia el próximo cubo. En el script asociado a los botones, hay un atributo <code>GameObject</code> que se llama <code>Next</code> este hace referenci al botón del que se debe guiar para instanciar el prefab cuando lo activen. También tiene un atributo <code>GameObject</code> que se llama <code>prefab</code> este hace referencia a cual objeto hay que destruir en el caso en que este botón sea el último de su saga o que tiene que instanciar . En el caso de tener un contacto con un cubo, entonces verifica si el next es nulo, si lo es, entonces destruye el prefab, si no lo es entonces crea una instancia de lo que tenga en prefab justo debajo de lo que tenga en next. </p>

<image
  src="GravityMaze/boton.png"
  width = 60%
  height = 60%>

<h2>Creando el Laberinto de Fase 2</h2>
<p1>Para crear nuestra fase 2, utilizamos ProBuilder para crear un plano de 30x30. Luego de darnos cuenta de que 30x30 no era suficiente, utilizamos la herramienta <code>Subdivide Object</code> para aumentar la cantidad de caras en nuestro plano. Ya satisfechos con la cantidad de caras, encontramos una imagen de un laberinto para utilizar como guia:</p1>

<image
src="FinalP/referenceLab.png"
width = 60%
height = 60%>

<p1>Ya con nuestra guia establecida, se construyeron las paredes seleccionando caras de tamaños distintos (usualmente de 3 a 10 caras de largo) hasta lograr tener CASI una replica 1:1 del laberinto, con algunos cambios para facilitar la salida del jugador.</p1> 

<image
src="FinalP/endLab.png"
width = 60%
height = 60%>

<p1>Por ultimo, utilizando prefabs de la fase anterior, colocamos los botones y puertas que desaparecen de acuerdo al progreso del player, abriendo lugares nuevos del laberinto para seguir explorando buscando el proximo boton. Esta parte del brainstorming fue divertida porque teniamos ideas distintas de dificultad pero concordamos con que el player debe de explorar casi el laberinto entero.</p1>

<h2>Creando la camara 3D</h2>
<p1>Para nuestra camara, utilizamos el package de Cinemachine para facilitar el control de parametros para nuestra camara. El estilo de camara que queriamos para la mayoria del juego era como la de Leon Kennedy en los juegos de Resident Evil 3 y Resident Evil 4, tercera persona pero un poco hacia el lado del hombro derecho de Leon:</p1>

<image
src="FinalP/LeonK.png"
width = 60%
height = 60%>

<p1>Para lograr este efecto, necesitamos solo una cosa mas ademas del <code>Main Camera</code>, necesitamos crear un <code>Right Click > Cinemachine > Virtual Camera</code> y colocarla debajo de nuestro Player Variant como un child de ese objeto. Luego, tenemos que <code>Drag & Drop > Follow | Drag & Drop > Look At</code> nuestro Player Variant a la camara virtual que colocamos debajo del prefab como child. Antes de poder trabajar con los parametros para la camara, aun no podemos verla, y esto es porque nos falta <code>Main Camera > Add Component > Cinemachine Brain</code> cual conecta nuestra camara hacia la camara virtual del jugador, y al tener este componente junta ambas camaras juntas y podemos controlar la Main Camera con los parametros de la virtual: </p1>

<image
src="FinalP/cam1.png"
width = 60%
height = 60%>

<image
src="FinalP/cam2.png"
width = 60%
height = 60%>

## Creando los fantasmas

A continuación, se enseñan los 2 prefabs que se hicieron para desarrollar el comportamiento de los fantasmas: el `RoamingGhost` para la fase 2 y el `Ghost` para el jefe.

Primero, el `Ghost`, que simplemente sigue al jugador en todo momento. Este prefab es instanciado todas las veces necesarias en la última fase.

<img src="img/09-ghost1.png" width=80%, height=80%>
<img src="img/10-ghost2.png" width=80%, height=80%>

Luego creamos el `RoamingGhost`, que tiene un componente de inteligencia artificial. Si el fantasma está cerca del jugador, va a perseguirlo. Si no, se dirigirá a algún botón preasignado. Solamente hay 5 de estos fantasmas instanciados "estáticamente" en la fase 2.

<img src="img/11-rghost1.png" width=80%, height=80%>
<img src="img/12-rghost2.png" width=80%, height=80%>
<img src="img/13-rghost3.png" width=80%, height=80%>
<img src="img/14-rghost4.png" width=80%, height=80%>
<img src="img/15-rghost5.png" width=80%, height=80%>

## Creación de la fase 3: el jefe final

La fase 3 consiste de un jefe que instanciará fantasmas infinitamente hasta que los 4 botones alrededor del campo de batalla hayan sido presionados. Cuando el último botón se presione, la plataforma debajo del jefe se eliminará y el jefe caerá al abismo, llevando al jugador a la victoria.

Iniciando la creación del escenario, añadimos un `Skybox` y creamos un campo de batalla en ProBuilder con una plataforma separada en el centro. Esta será la plataforma que "colapsará" al final del juego.

<img src="img/01-skybox.png" width=80%, height=80%>
<img src="img/02-arena.png" width=80%, height=80%>

Ubicamos los botones y al jugador alrededor del mapa...

<img src="img/03-buttonlighting.png" width=80%, height=80%>
<img src="img/04-player.png" width=80%, height=80%>

Instanciamos al jefe como un fantasma gigantesco. Creamos un script para su comportamiento. Solamente mirará al jugador a todo momento y matará al jugador si entra en contacto con él.

<img src="img/05-boss1.png" width=80%, height=80%>
<img src="img/05-boss2.png" width=80%, height=80%>

Ahora creamos un `Spawner` de fantasmas de tal manera que aparezcan alrededor de todo el campo de batalla. La técnica para esparcir los fantasmas es la misma utilizada para la lluvia en el pasado _Challenge 6_.

<img src="img/06-spawner1.png" width=80%, height=80%>
<img src="img/07-spawner2.png" width=80%, height=80%>

Finalmente, decoramos un poco el campo de batalla añadiendo `Particle Systems` de fuego alrededor de la plataforma central.

<img src="img/08-fire.png" width=80%, height=80%>

El resultado final es el siguiente:

<img src="img/final.png" width=80%, height=80%>

<h2>Fin de Juego</h2>
<p1>Para crear las escenas de fin de juego, utilizamos lo aprendido en clase y creamos dos imagenes AI con relacion al videojuego, y creamos dos escenas <code>Defeat and Victory</code> con un cubo que aguantara nuestras imagenes y una camara ajustada para que la imagen sea el centro de su vision.</p1>

<image
src="FinalP/VICTORY.jpeg"
width = 60%
height = 60%>

<image
src="FinalP/DEFEAT.jpeg"
width = 60%
height = 60%>
















