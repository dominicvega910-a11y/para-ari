
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Para Ari 💗</title>

<style>
* { box-sizing: border-box; }

body {
  margin: 0;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  font-family: Georgia, serif;
  color: #8d3155;
  background: linear-gradient(135deg, #ffe4ef, #fff7fa, #ffc9df);
  overflow-x: hidden;
}

.card {
  width: 100%;
  max-width: 440px;
  padding: 32px 23px;
  text-align: center;
  background: #ffffffdf;
  border: 1px solid white;
  border-radius: 28px;
  box-shadow: 0 15px 50px #d64c7b30;
  position: relative;
  z-index: 2;
}

.heart {
  font-size: 65px;
  animation: latir 1.3s infinite;
}

h1 {
  font-size: 32px;
  color: #d63375;
  line-height: 1.2;
}

p {
  font-size: 17px;
  line-height: 1.7;
}

button {
  border: none;
  border-radius: 30px;
  padding: 14px 21px;
  margin: 6px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

#si {
  background: #ed4383;
  color: white;
  box-shadow: 0 5px 15px #ed438344;
}

#no {
  color: #b83b69;
  background: #ffe0ec;
}

#musica {
  background: #fff0f6;
  color: #b83b69;
  margin-top: 15px;
}

.firma {
  font-size: 14px;
  color: #c47796;
  margin-top: 24px;
}

.flotante {
  position: fixed;
  bottom: -30px;
  animation: subir linear forwards;
  pointer-events: none;
  z-index: 1;
}

@keyframes latir {
  50% { transform: scale(1.13); }
}

@keyframes subir {
  to { transform: translateY(-110vh) rotate(25deg); opacity: 0; }
}
</style>
</head>

<body>

<div class="card" id="tarjeta">
  <div class="heart">💗</div>

  <p>Hay algo que llevo tiempo queriendo decirte...</p>

  <h1>ARI, ¿QUIERES SER MI NOVIA? 🥹💕</h1>

  <p>
    Quiero que sepas que eres alguien muy especial para mí.
    Me encanta hablar contigo y quisiera seguir compartiendo
    momentos bonitos a tu lado.
  </p>

  <h2>¿Quieres ser mi novia y hacerme el niño más feliz? 💘</h2>

  <div>
    <button id="si" onclick="aceptar()">¡SÍÍÍ! 💖</button>
    <button id="no" onclick="respuestaNo()">No 🥺</button>
  </div>

  <button id="musica" onclick="musicaToggle()">
    🎵 Activar musiquita
  </button>

  <div class="firma">Hecho con mucho cariño, para Ari 🌷</div>
</div>

<script>
let audio;
let osciladores = [];
let sonando = false;
let temporizador;

function musicaToggle() {
  if (sonando) {
    clearInterval(temporizador);
    osciladores.forEach(o => {
      try { o.stop(); } catch(e) {}
    });
    osciladores = [];
    sonando = false;
    document.getElementById("musica").textContent =
      "🎵 Activar musiquita";
    return;
  }

  const AudioContext =
    window.AudioContext || window.webkitAudioContext;

  if (!AudioContext) {
    alert("Tu navegador no permite reproducir esta música.");
    return;
  }

  audio = new AudioContext();
  audio.resume();
  sonando = true;

  document.getElementById("musica").textContent =
    "🔇 Apagar musiquita";

  // Melodía suave creada con sonidos del navegador.
  const notas = [523.25, 659.25, 783.99, 659.25,
                 587.33, 698.46, 880, 698.46];
  let i = 0;

  function nota() {
    if (!sonando) return;

    const osc = audio.createOscillator();
    const volumen = audio.createGain();

    osc.type = "sine";
    osc.frequency.value = notas[i % notas.length];

    volumen.gain.setValueAtTime(0.0001, audio.currentTime);
    volumen.gain.exponentialRampToValueAtTime(
      0.07, audio.currentTime + 0.08
    );
    volumen.gain.exponentialRampToValueAtTime(
      0.0001, audio.currentTime + 0.6
    );

    osc.connect(volumen);
    volumen.connect(audio.destination);
    osc.start();
    osc.stop(audio.currentTime + 0.65);

    i++;
  }

  nota();
  temporizador = setInterval(nota, 650);
}

function respuestaNo() {
  const boton = document.getElementById("no");
  const mensajes = [
    "¿Lo pensás un poquito más? 💗",
    "Está bien, Ari 🥺",
    "Quería preguntártelo con cariño 💕"
  ];

  boton.textContent =
    mensajes[Math.floor(Math.random() * mensajes.length)];
}

function aceptar() {
  document.getElementById("tarjeta").innerHTML = `
    <div class="heart">💖</div>
    <h1>¡ARI DIJO QUE SÍÍÍ! 😭💗</h1>
    <p>
      No sabes lo feliz que me hace esto.
      Gracias por darme esta oportunidad.
      Quiero que construyamos recuerdos hermosos,
      que nos riamos juntos y que nos apoyemos siempre.
    </p>
    <h2>Te quiero muchísimo, princesa 💘</h2>
    <p>Esto es el comienzo de algo muy bonito. 🫶</p>
    <div style="font-size:32px">🌷💗🌷💗🌷</div>
    <p class="firma">Con cariño, para Ari ❤️</p>
  `;

  for (let i = 0; i < 55; i++) {
    const corazon = document.createElement("div");
    corazon.className = "flotante";
    corazon.textContent =
      ["💗", "💕", "💖", "💘", "🌸"][
        Math.floor(Math.random() * 5)
      ];
    corazon.style.left = Math.random() * 100 + "vw";
    corazon.style.fontSize = (18 + Math.random() * 22) + "px";
    corazon.style.animationDuration = (3 + Math.random() * 4) + "s";
    document.body.appendChild(corazon);

    setTimeout(() => corazon.remove(), 7500);
  }

  if (!sonando) musicaToggle();
}

setInterval(() => {
  const corazon = document.createElement("div");
  corazon.className = "flotante";
  corazon.textContent = ["♡", "💕", "💗", "🌸"][
    Math.floor(Math.random() * 4)
  ];
  corazon.style.left = Math.random() * 100 + "vw";
  corazon.style.fontSize = (16 + Math.random() * 20) + "px";
  corazon.style.animationDuration = (6 + Math.random() * 5) + "s";
  document.body.appendChild(corazon);
  setTimeout(() => corazon.remove(), 12000);
}, 800);
</script>

</body>
</html>
# para-ari