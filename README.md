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


FOTO DE PRIMER LABERINTO




<h2>Manejo de input y animaciones</h2>

<p> Previamente configuramos el movimiento de nuestro jugador utilzando el <code>New Input System</code>. Con esto hecho, uno de los primeros retos que decidimos enfrentar fue manejar que cada animación se presentara en el momento adecuado. Para esto básicamente generamos una máquina de estados finitos creando dentro de un <code>Animation controller</code>.</p>


GIF DE ANIMACIONES








<h2>Bala que rebota las paredes.</h2>

<p>Otro de los factores que el jugador debe tener en cuenta es que si una de sus balas choca una pared la bala rebotará y le afectará. </p>

GIF DE BALA QUE REBOTA 




<h2>Self Gravity Shift</h2>

<p>Para dar más dinamismo al juego será posible activar un modo de "Gravity Shift" al presionar el <code>Space bar</code>.</p>

GIF DE GRAVITY SHIFT




























