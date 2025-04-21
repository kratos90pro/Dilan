# Dilan
Juego casino
<!DOCTYPE html><html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CasinoAmigazo</title>
  <style>
    body {
      margin: 0;
      font-family: sans-serif;
      background-color: #000;
      color: #fff;
    }
    header {
      background-color: #111;
      padding: 1rem;
      text-align: center;
    }
    nav ul {
      list-style: none;
      display: flex;
      justify-content: center;
      padding: 0;
    }
    nav ul li {
      margin: 0 1rem;
    }
    nav ul li a {
      color: #fff;
      text-decoration: none;
    }
    section {
      padding: 2rem;
    }
    .juego {
      background-color: #222;
      padding: 1rem;
      margin: 1rem 0;
      border-radius: 10px;
    }
    form input, form button, .juego select, .juego button {
      display: block;
      width: 100%;
      margin: 0.5rem 0;
      padding: 0.5rem;
      border-radius: 5px;
      border: none;
    }
    form button, .juego button {
      background-color: #444;
      color: #fff;
      cursor: pointer;
    }
    footer {
      background-color: #111;
      text-align: center;
      padding: 1rem;
      position: fixed;
      width: 100%;
      bottom: 0;
    }
    .cartas {
      display: flex;
      gap: 1rem;
      margin-top: 1rem;
    }
    .carta {
      background-color: #333;
      padding: 1rem;
      border-radius: 8px;
      text-align: center;
      width: 100px;
    }
  </style>
</head>
<body>
  <header>
    <h1>CasinoAmigazo</h1>
    <nav>
      <ul>
        <li><a href="#inicio">Inicio</a></li>
        <li><a href="#juegos">Juegos</a></li>
        <li><a href="#login">Iniciar Sesión</a></li>
        <li><a href="#registro">Registrarse</a></li>
      </ul>
    </nav>
  </header>  <section id="inicio">
    <h2>Bienvenido a CasinoAmigazo</h2>
    <p>Comenzá con 5.000 guaraníes y disfrutá de todos los juegos de casino. Recargá vía WhatsApp.</p>
  </section>  <section id="juegos">
    <h2>Juegos de Casino</h2>
    <div class="juego">
      <h3>Hilo de Cartas</h3>
      <p>Elegí si la próxima carta será mayor o menor. Si acertás, ganás el doble.</p>
      <label for="apuesta">Monto a apostar (saldo actual: <span id="saldo">5000</span> Gs):</label>
      <select id="apuesta">
        <option value="500">500 Gs</option>
        <option value="600">600 Gs</option>
        <option value="700">700 Gs</option>
        <option value="800">800 Gs</option>
        <option value="1000">1000 Gs</option>
        <option value="2000">2000 Gs</option>
        <option value="3000">3000 Gs</option>
        <option value="4000">4000 Gs</option>
        <option value="5000">5000 Gs</option>
        <option value="10000">10000 Gs</option>
        <option value="20000">20000 Gs</option>
        <option value="30000">30000 Gs</option>
        <option value="40000">40000 Gs</option>
        <option value="50000">50000 Gs</option>
      </select>
      <button onclick="jugarHilo()">Sacar carta</button>
      <div id="cartasHilo" class="cartas"></div>
      <div id="opcionesHilo" style="margin-top: 1rem; display: none;">
        <button onclick="apostar('mayor')">Mayor</button>
        <button onclick="apostar('menor')">Menor</button>
      </div>
      <p id="resultadoHilo"></p>
    </div>
    <div class="juego">Tragamonedas (en desarrollo)</div>
    <div class="juego">Ruleta (en desarrollo)</div>
    <div class="juego">Blackjack (en desarrollo)</div>
  </section>  <section id="login">
    <h2>Iniciar Sesión</h2>
    <form onsubmit="login(event)">
      <input type="text" id="usuario" placeholder="Usuario" required>
      <input type="password" id="password" placeholder="Contraseña" required>
      <button type="submit">Entrar</button>
    </form>
    <p id="mensajeLogin"></p>
  </section>  <section id="registro">
    <h2>Registro solo por administrador</h2>
    <p>Contactá con el administrador para crear tu cuenta.</p>
  </section>  <footer>
    <p>&copy; 2025 CasinoAmigazo - Todos los derechos reservados</p>
  </footer>  <script>
    let saldo = 5000;
    let cartaActual = null;
    let apuesta = 0;

    function login(e) {
      e.preventDefault();
      const usuario = document.getElementById('usuario').value;
      const password = document.getElementById('password').value;

      if (usuario === 'kratos90pro' && password === 'kratos320') {
        document.getElementById('mensajeLogin').innerText = 'Inicio de sesión exitoso (Administrador)';
        alert('Bienvenido, administrador!');
      } else {
        document.getElementById('mensajeLogin').innerText = 'Usuario o contraseña incorrectos';
      }
    }

    function actualizarSaldo() {
      document.getElementById('saldo').innerText = saldo;
    }

    function jugarHilo() {
      apuesta = parseInt(document.getElementById('apuesta').value);
      if (isNaN(apuesta) || apuesta < 500 || apuesta > saldo) {
        alert("Apuesta inválida.");
        return;
      }
      cartaActual = Math.floor(Math.random() * 13) + 1;
      document.getElementById('cartasHilo').innerHTML = `<div class='carta'>${cartaActual}</div>`;
      document.getElementById('resultadoHilo').innerText = '';
      document.getElementById('opcionesHilo').style.display = 'block';
    }

    function apostar(opcion) {
      const nuevaCarta = Math.floor(Math.random() * 13) + 1;
      document.getElementById('cartasHilo').innerHTML += `<div class='carta'>${nuevaCarta}</div>`;

      let gano = false;
      if (opcion === 'mayor' && nuevaCarta > cartaActual) gano = true;
      if (opcion === 'menor' && nuevaCarta < cartaActual) gano = true;

      if (gano) {
        saldo += apuesta;
        document.getElementById('resultadoHilo').innerText = '¡Ganaste! +'+apuesta+' Gs';
      } else {
        saldo -= apuesta;
        document.getElementById('resultadoHilo').innerText = 'Perdiste -'+apuesta+' Gs';
      }
      actualizarSaldo();
      document.getElementById('opcionesHilo').style.display = 'none';
    }

    actualizarSaldo();
  </script></body>
</html>
