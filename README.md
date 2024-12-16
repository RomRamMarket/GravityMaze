# GravityMaze

<h1>Requerimientos</h1>

<ul>
  <li>Insatalar <code>ProBuilder</code>.</li>
  <li>Configurar <code>New input system</code>.</li>
  <li>Importar paquete <code>Battle Wizard Poly Art</code> del asset store.</li>
  <li>Importar paquete <code>Little Ghost lowpoly(FREE)</code> del asset store.</li>
</ul>


<h2>Contexto</h2>

<p>AQUI DEBERIAMOS EXPLICAR UN POCO EL CONTEXTO DE NUESTRO JUEGO. DINAMICA, TEMATICA, OBJETIVO, INSPIRACION...</p>


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



<image
  src="GravityMaze/esquema.png"
  width = 60%
  height = 60%>

<image
  src="GravityMaze/gameplay1.gif"
  width = 60%
  height = 60%>




  


<h2>Cómo se conoce donde se debe instanciar el próximo cubo?</h2>

<p>Los objetos tipo "cubo" tienen asociados un script que solo detecta si hubo un collider de parte de la bala del player y le "cambia" la gravedad. En la práctica solo le aumenta la velocidad en dirección hacia arriba. Cuando choca con un botón deja de subir. </p>

<image
  src="GravityMaze/cubo.png"
  width = 60%
  height = 60%>

















