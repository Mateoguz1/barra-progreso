<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Objetivo Semanal</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', sans-serif;
      background: #0a0f2c;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
    }

    h1 {
      font-size: 3rem;
      margin-bottom: 40px;
      letter-spacing: 1.5px;
    }

    .porcentaje {
      font-size: 2.5rem;
      margin-bottom: 20px;
      color: #00ffe7;
      font-weight: bold;
    }

    .barra-container {
      width: 80%;
      max-width: 900px;
      height: 40px;
      background-color: rgba(255, 255, 255, 0.08);
      border-radius: 30px;
      overflow: hidden;
      box-shadow: 0 0 20px #00f0ff44;
      margin-bottom: 10px;
    }

    .barra {
      height: 100%;
      width: 0%;
      background: linear-gradient(to right, #00f0ff, #ff00ff);
      box-shadow: 0 0 20px #00f0ff, 0 0 30px #ff00ff;
      transition: width 0.8s ease;
      border-radius: 30px;
    }

    .marcadores {
      display: flex;
      justify-content: space-between;
      width: 80%;
      max-width: 900px;
      margin: 10px 0 30px 0;
      font-size: 1rem;
      color: #ccc;
    }

    input[type="number"] {
      background: rgba(255, 255, 255, 0.1);
      border: none;
      border-radius: 10px;
      padding: 12px 20px;
      font-size: 1.2rem;
      color: #fff;
      outline: none;
      width: 180px;
      text-align: center;
      box-shadow: 0 0 10px #ffffff22;
    }
  </style>
</head>
<body>

  <h1>OBJETIVO SEMANAL</h1>

  <div class="porcentaje" id="porcentaje-texto">0%</div>

  <div class="barra-container">
    <div id="barra" class="barra"></div>
  </div>

  <div class="marcadores">
    <span>$1K</span>
    <span>$10K</span>
  </div>

  <input type="number" id="cash" placeholder="Ingresar monto" oninput="actualizarBarra()" />

  <script>
    const meta = 10000;

    function actualizarBarra() {
      const input = document.getElementById("cash").value;
      const cash = parseFloat(input);
      if (isNaN(cash)) return;

      const porcentaje = Math.min((cash / meta) * 100, 100);
      const barra = document.getElementById("barra");
      const texto = document.getElementById("porcentaje-texto");

      barra.style.width = porcentaje + "%";
      texto.textContent = Math.floor(porcentaje) + "%";

      localStorage.setItem("cash", cash);
      localStorage.setItem("ultimaActualizacion", new Date().toString());
    }

    // Reinicio automático los lunes
    const hoy = new Date();
    const ultimoUpdate = localStorage.getItem("ultimaActualizacion");
    if (ultimoUpdate) {
      const ultimaFecha = new Date(ultimoUpdate);
      const esNuevoLunes = hoy.getDay() === 1 && hoy.toDateString() !== ultimaFecha.toDateString();
      if (esNuevoLunes) {
        localStorage.removeItem("cash");
        localStorage.setItem("ultimaActualizacion", hoy.toString());
      }
    } else {
      localStorage.setItem("ultimaActualizacion", hoy.toString());
    }

    // Cargar al inicio
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
