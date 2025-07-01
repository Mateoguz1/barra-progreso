<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Progreso Semanal</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      overflow: hidden;
    }

    h1 {
      font-size: 2rem;
      margin-bottom: 30px;
      font-weight: 500;
    }

    .porcentaje {
      font-size: 2.5rem;
      font-weight: bold;
      margin-bottom: 20px;
    }

    .barra-container {
      width: 80%;
      max-width: 700px;
      height: 25px;
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 20px;
      overflow: hidden;
      box-shadow: 0 0 10px #00ffff44;
    }

    .barra {
      height: 100%;
      width: 0%;
      background: linear-gradient(to right, #00c6ff, #0072ff);
      border-radius: 20px;
      transition: width 0.5s ease;
    }

    .etiquetas {
      display: flex;
      justify-content: space-between;
      width: 80%;
      max-width: 700px;
      margin-top: 15px;
      font-size: 0.85rem;
      color: #ccc;
    }
  </style>
</head>
<body>

  <h1>Cash Collected</h1>
  <div class="porcentaje" id="porcentaje-texto">0%</div>

  <div class="barra-container">
    <div id="barra" class="barra"></div>
  </div>

  <div class="etiquetas">
    <span>$1K</span><span>$2K</span><span>$3K</span><span>$4K</span><span>$5K</span>
    <span>$6K</span><span>$7K</span><span>$8K</span><span>$9K</span><span>$10K</span>
  </div>

  <script>
    const meta = 10000;

    // Simular carga automática
    const cashGuardado = localStorage.getItem("cash") || "0";

    function actualizarBarra(cash) {
      const porcentaje = Math.min((cash / meta) * 100, 100);
      const barra = document.getElementById("barra");
      barra.style.width = porcentaje + "%";
      document.getElementById("porcentaje-texto").textContent = Math.floor(porcentaje) + "%";
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

    // Cargar y mostrar
    actualizarBarra(parseFloat(localStorage.getItem("cash") || 0));
  </script>

</body>
</html>
