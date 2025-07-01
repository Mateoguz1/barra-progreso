<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Progreso Semanal</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #a8edea, #fed6e3);
      margin: 0;
      padding: 40px;
      text-align: center;
      color: #333;
    }

    h1 {
      margin-bottom: 10px;
    }

    .barra-container {
      position: relative;
      width: 80%;
      max-width: 700px;
      margin: 40px auto 10px auto;
      background-color: #eee;
      border-radius: 25px;
      height: 35px;
      overflow: hidden;
      box-shadow: 0 3px 10px rgba(0,0,0,0.1);
    }

    .barra {
      height: 100%;
      background: linear-gradient(to right, #06beb6, #48b1bf);
      width: 0%;
      border-radius: 25px 0 0 25px;
      text-align: right;
      color: white;
      line-height: 35px;
      padding-right: 10px;
      box-sizing: border-box;
      transition: width 0.6s ease-in-out;
    }

    .etiquetas {
      display: flex;
      justify-content: space-between;
      width: 80%;
      max-width: 700px;
      margin: 10px auto;
      font-size: 0.9em;
      color: #444;
    }

    .info {
      margin-top: 10px;
      font-size: 1.1em;
    }

    input[type="number"] {
      padding: 8px;
      width: 120px;
      margin-right: 10px;
      border-radius: 5px;
      border: 1px solid #aaa;
    }

    button {
      padding: 8px 15px;
      background-color: #48b1bf;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #369da6;
    }

    .mensaje-exito {
      color: green;
      font-weight: bold;
      margin-top: 10px;
    }
  </style>
</head>
<body>

<h1>Cash Collected esta semana</h1>

<div class="barra-container">
  <div id="barra" class="barra">0%</div>
</div>

<div class="etiquetas">
  <span>$1K</span><span>$2K</span><span>$3K</span><span>$4K</span><span>$5K</span><span>$6K</span><span>$7K</span><span>$8K</span><span>$9K</span><span>$10K</span>
</div>

<div class="info">
  <label for="cash">Ingresar cash ($): </label>
  <input type="number" id="cash" value="0">
  <button onclick="actualizarBarra()">Actualizar</button>
</div>

<div id="mensaje" class="mensaje-exito"></div>

<script>
  const meta = 10000;

  function actualizarBarra() {
    const input = document.getElementById("cash").value;
    const cash = parseFloat(input);
    const porcentaje = Math.min((cash / meta) * 100, 100);
    const barra = document.getElementById("barra");
    barra.style.width = porcentaje + "%";
    barra.textContent = Math.floor(porcentaje) + "%";

    localStorage.setItem("cash", cash);
    localStorage.setItem("ultimaActualizacion", new Date().toString());

    const mensaje = document.getElementById("mensaje");
    if (porcentaje >= 100) {
      mensaje.textContent = "🎉 ¡Meta alcanzada!";
    } else {
      mensaje.textContent = `$${cash.toLocaleString()} recaudados de $10,000`;
    }
  }

  // Reinicio automático los lunes
  const hoy = new Date();
  const ultimoUpdate = localStorage.getItem("ultimaActualizacion");

  if (ultimoUpdate) {
    const ultimaFecha = new Date(ultimoUpdate);
    const esLunes = hoy.getDay() === 1;
    const esNuevoLunes = esLunes && hoy.toDateString() !== ultimaFecha.toDateString();
    if (esNuevoLunes) {
      localStorage.removeItem("cash");
      localStorage.setItem("ultimaActualizacion", hoy.toString());
    }
  } else {
    localStorage.setItem("ultimaActualizacion", hoy.toString());
  }

  // Cargar progreso al inicio
  window.onload = () => {
    const cashGuardado = localStorage.getItem("cash");
    if (cashGuardado !== null) {
      document.getElementById("cash").value = cashGuardado;
      actualizarBarra();
    }
  };
</script>

</body>
</html>
