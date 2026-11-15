# DESARROLLO-SUSTENTABLE

<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Huella energetica de la nube</title>
<style>
  :root {
    --bosque: #1f4d3a;
    --musgo: #3f7d58;
    --hoja: #8cc084;
    --arena: #f3efe2;
    --agua: #2b7a8c;
    --tierra: #6b5a3e;
    --tinta: #1c2a24;
    --blanco: #fffdf7;
    --error: #a63d2f;
  }
  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    margin: 0;
    font-family: "Trebuchet MS", "Segoe UI", system-ui, sans-serif;
    color: var(--tinta);
    background: var(--arena);
    line-height: 1.55;
  }
  header {
    background:
      radial-gradient(circle at 85% 20%, rgba(140,192,132,.35), transparent 45%),
      linear-gradient(160deg, var(--bosque), #14352a);
    color: var(--blanco);
    padding: 3rem 1.25rem 4.5rem;
  }
  .contenedor { max-width: 760px; margin: 0 auto; }
  h1 {
    font-family: Georgia, "Times New Roman", serif;
    font-size: clamp(2rem, 6vw, 3.1rem);
    line-height: 1.1;
    margin: 0 0 1rem;
    font-weight: 700;
    letter-spacing: -.01em;
  }
  header p { margin: 0; max-width: 58ch; font-size: 1.05rem; color: #dcebd9; }
  main { margin-top: -2.5rem; padding: 0 1.25rem 3rem; }
  .tarjeta {
    background: var(--blanco);
    border: 1px solid #d9d2bd;
    border-radius: 14px;
    padding: 1.5rem;
    box-shadow: 0 10px 30px rgba(31,77,58,.12);
  }
  fieldset { border: 0; padding: 0; margin: 0 0 1.5rem; }
  legend {
    font-family: Georgia, serif;
    font-size: 1.2rem;
    color: var(--bosque);
    font-weight: 700;
    padding: 0;
    margin-bottom: .75rem;
    border-bottom: 2px solid var(--hoja);
    width: 100%;
    padding-bottom: .35rem;
  }
  .grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1rem 1.25rem; }
  .campo { display: flex; flex-direction: column; }
  .campo label { font-weight: 700; font-size: .95rem; margin-bottom: .15rem; }
  .campo small { color: #5a6b62; font-size: .82rem; margin-bottom: .4rem; }
  input[type="number"] {
    font: inherit;
    padding: .6rem .75rem;
    border: 1.5px solid #b9c4b0;
    border-radius: 8px;
    background: #fff;
    color: var(--tinta);
    width: 100%;
  }
  input[type="number"]:focus-visible,
  button:focus-visible {
    outline: 3px solid var(--agua);
    outline-offset: 2px;
  }
  button {
    font: inherit;
    font-weight: 700;
    font-size: 1.05rem;
    width: 100%;
    padding: .9rem 1rem;
    border: 0;
    border-radius: 10px;
    background: var(--musgo);
    color: #fff;
    cursor: pointer;
    transition: background .2s;
  }
  button:hover:not(:disabled) { background: var(--bosque); }
  button:disabled { background: #8a9a90; cursor: wait; }
  #resultado {
    margin-top: 1.5rem;
    padding: 1.1rem 1.25rem;
    border-left: 6px solid var(--agua);
    background: #eaf4f2;
    border-radius: 8px;
    white-space: pre-line;
    overflow-wrap: anywhere;
    font-size: .98rem;
  }
  #resultado.error { border-left-color: var(--error); background: #f9e9e6; color: var(--error); font-weight: 700; }
  #resultado.espera { color: #3d5a63; font-style: italic; }
  [hidden] { display: none !important; }
  footer { text-align: center; font-size: .85rem; color: #5a6b62; padding: 0 1rem 2rem; }
  @media (max-width: 560px) {
    .grid { grid-template-columns: 1fr; }
    header { padding-top: 2rem; }
    .tarjeta { padding: 1.1rem; }
  }
  @media (prefers-reduced-motion: reduce) {
    * { transition: none !important; scroll-behavior: auto !important; }
  }
</style>
</head>
<body>

<header>
  <div class="contenedor">
    <h1>Huella energética de la nube</h1>
    <p>Cada acción digital, como ver un video, subir una foto o preguntarle algo a una IA, se procesa en centros de datos que consumen energía. Esta página estima tu huella a partir de tu uso semanal.</p>
  </div>
</header>

<main>
  <div class="contenedor tarjeta">
    <form id="formulario">
      <fieldset>
        <legend>Lo que haces cada día</legend>
        <div class="grid">
          <div class="campo">
            <label for="video">Video en streaming</label>
            <small>Horas al día en YouTube, Netflix, TikTok</small>
            <input type="number" id="video" name="video" min="0" step="any" value="0" required>
          </div>
          <div class="campo">
            <label for="musica">Música en streaming</label>
            <small>Horas al día</small>
            <input type="number" id="musica" name="musica" min="0" step="any" value="0" required>
          </div>
          <div class="campo">
            <label for="redes">Redes sociales</label>
            <small>Horas al día</small>
            <input type="number" id="redes" name="redes" min="0" step="any" value="0" required>
          </div>
          <div class="campo">
            <label for="juegos">Juegos en línea</label>
            <small>Horas al día</small>
            <input type="number" id="juegos" name="juegos" min="0" step="any" value="0" required>
          </div>
          <div class="campo">
            <label for="ia">Chatbots de IA</label>
            <small>Consultas al día</small>
            <input type="number" id="ia" name="ia" min="0" step="any" value="0" required>
          </div>
          <div class="campo">
            <label for="correos">Correos enviados</label>
            <small>Correos al día</small>
            <input type="number" id="correos" name="correos" min="0" step="any" value="0" required>
          </div>
        </div>
      </fieldset>

      <fieldset>
        <legend>Lo que haces cada semana y lo que guardas</legend>
        <div class="grid">
          <div class="campo">
            <label for="videollamadas">Videollamadas</label>
            <small>Horas a la semana</small>
            <input type="number" id="videollamadas" name="videollamadas" min="0" step="any" value="0" required>
          </div>
          <div class="campo">
            <label for="nube">Almacenamiento en la nube</label>
            <small>GB guardados (fotos, archivos)</small>
            <input type="number" id="nube" name="nube" min="0" step="any" value="0" required>
          </div>
        </div>
      </fieldset>

      <button type="submit" id="boton">Calcular mi huella</button>
    </form>

    <div id="resultado" role="status" aria-live="polite" hidden></div>
  </div>
</main>

<footer>Desarrollo Sustentable · Instituto Tecnológico de Mazatlán</footer>

<script>
  // Pega aquí la URL de tu webhook de Make (Webhooks > Custom webhook)
  const WEBHOOK_URL = "https://hook.eu1.make.com/txp1j4w9ea7q38sgrg1gvxdbn6jrxkan";

  const CAMPOS = ["video", "musica", "redes", "videollamadas", "juegos", "nube", "ia", "correos"];

  const formulario = document.getElementById("formulario");
  const boton = document.getElementById("boton");
  const resultado = document.getElementById("resultado");

  function mostrar(texto, clase) {
    resultado.hidden = false;
    resultado.className = clase || "";
    resultado.textContent = texto;
  }

  formulario.addEventListener("submit", async function (e) {
    e.preventDefault();

    const datos = new URLSearchParams();
    CAMPOS.forEach(function (nombre) {
      const valor = parseFloat(document.getElementById(nombre).value);
      datos.append(nombre, isNaN(valor) || valor < 0 ? 0 : valor);
    });

    boton.disabled = true;
    boton.textContent = "Calculando...";
    mostrar("Calculando...", "espera");

    try {
      const respuesta = await fetch(WEBHOOK_URL, {
        method: "POST",
        body: datos
      });
      if (!respuesta.ok) throw new Error("HTTP " + respuesta.status);
      const texto = await respuesta.text();
      if (!texto.trim()) throw new Error("Respuesta vacía");
      mostrar(texto.trim());
      resultado.scrollIntoView({ behavior: "smooth", block: "nearest" });
    } catch (error) {
      mostrar("No se pudo calcular, intenta de nuevo.", "error");
    } finally {
      boton.disabled = false;
      boton.textContent = "Calcular mi huella";
    }
  });
</script>
</body>
</html>
