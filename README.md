<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Objetivo Semanal</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: #0a0f2c;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      color: #fff;
    }

    h1 {
      font-size: 3rem;
      margin-bottom: 40px;
      color: #ffffffcc;
      text-transform: uppercase;
      letter-spacing: 2px;
    }

    .input-box {
      margin-bottom: 40px;
    }

    input[type="number"] {
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid #ffffff33;
      border-radius: 10px;
      padding: 15px 20px;
      font-size: 1.5rem;
      color: #fff;
      outline: none;
      width: 200px;
      text-align: center;
    }

    .barra-container {
      width: 90%;
      max-width: 900px;
      background-color: rgba(255, 255, 255, 0.08);
      border-radius: 50px;
      height: 35px;
      overflow: hidden;
      box-shadow: 0 0 15px #0ff;
      position: relative;
    }

    .barra {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #00f0ff, #ff00ff);
      box-shadow: 0 0 15px #00f0ff, 0 0 30px #ff00ff;
      transition: width 0.8s ease;
      border-radius: 50px;
    }

    .marcadores {
      display: flex;
      justify-content: space-between;
      width: 90%;
      max-width: 900px;
      margin-top: 15px;
      font-size: 1rem;
      color: #aaa;
      letter-spacing: 1px;
    }

    .porcentaje {
      font-size: 2rem;
      margin: 20px 0 10px;
      color: #0ff;
    }
  </style>
</head>
<body>

  <h1>Objetivo semanal</h1>

  <div class="input-box">
    <input type="number" id="cash" placeholder="Ingresar monto" oninput="actualizarBarra()" />
  </div>

  <div class="porcentaje" id="porcentaje-texto">0%</div>

  <div class="barra-container">
    <div id="barra" class="barra"></div>
  </div>

  <div class="marcadores">
    <span>$1K</span><span>$2K</span><span>$3K</span><span>$4K</span><span>$5K</span>
    <span>$6K</span><span>$7K</span><span>$8K</span><span>$9K</span><span>$10K</span>
  </div>

  <script>
    const meta = 10000;

    function actualizarBarra() {
      const input = document.getElementById("cash").value;
      const cash = parseFloat(input);
      const porcentaje = Math.min((cash / meta) * 100, 100);
      const barra = document.getElementById("barra");
      const texto = document.getElementById("porcentaje-texto");

      barra.style.width = porcentaje + "%";
      texto.textContent = Math.floor(porcentaje) + "%";

      localStorage.setItem("cash", cash);
      localStorage.setItem("ultimaActualizacion", new Date().toString());
    }

    // Reinicio automático cada lunes
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

    // Cargar valor guardado
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
