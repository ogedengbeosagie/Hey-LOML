# Hey-LOML
Valentine - 2026
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Valentine Proposal</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
:root {
  --purple-dark: #4b1fa6;
  --purple-main: #7b3fe4;
  --purple-soft: #c6a9ff;
  --purple-bg: #12061f;
  --white: #ffffff;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: system-ui, sans-serif;
  background: radial-gradient(circle at top, var(--purple-main), var(--purple-bg));
  color: var(--white);
  height: 100vh;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

canvas {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 5;
}

.card {
  background: linear-gradient(180deg, #2a0d52, #1a082f);
  border-radius: 22px;
  padding: 32px 26px;
  width: 340px;
  text-align: center;
  box-shadow: 0 20px 60px rgba(0,0,0,0.45);
  position: relative;
  z-index: 10;
}

h1 {
  font-size: 20px;
  margin: 18px 0 14px;
}

.zone {
  display: flex;
  gap: 16px;
  justify-content: center;
  margin-top: 16px;
}

button {
  border: none;
  padding: 12px 20px;
  border-radius: 999px;
  font-size: 15px;
  font-weight: 600;
  cursor: pointer;
}

#yesBtn {
  background: var(--purple-main);
  color: var(--white);
}

#noBtn {
  background: transparent;
  color: var(--purple-soft);
  border: 1px solid var(--purple-soft);
  position: relative;
}

.hint {
  margin-top: 14px;
  font-size: 13px;
  color: var(--purple-soft);
  display: none;
}

.result {
  display: none;
}

.result h2 {
  font-size: 26px;
  margin-bottom: 6px;
}

.result p {
  font-size: 15px;
  color: var(--purple-soft);
}
</style>
</head>

<body>

<canvas id="confettiCanvas"></canvas>

<main class="card" id="card">
  <svg class="art" viewBox="0 0 320 240" width="220">
    <defs>
      <linearGradient id="heartGrad" x1="0" x2="1">
        <stop offset="0%" stop-color="#b07cff"/>
        <stop offset="100%" stop-color="#7b3fe4"/>
      </linearGradient>
    </defs>
    <path d="M160 190 C40 120, 80 40, 160 90 C240 40, 280 120, 160 190 Z"
          fill="url(#heartGrad)"/>
  </svg>

  <h1>Onyinyechi, will you be my Valentine?</h1>

  <section class="zone" id="zone">
    <button id="yesBtn">Yes 💜</button>
    <button id="noBtn">No</button>
  </section>

  <div class="hint" id="hint">The 'No' button likes shakara like you 😈</div>

  <section class="result" id="result">
    <h2>SHARP!! 😂🎉💜</h2>
    <p>Osagie.</p>
  </section>
</main>

<script>
const yesBtn = document.getElementById("yesBtn");
const noBtn = document.getElementById("noBtn");
const zone = document.getElementById("zone");
const hint = document.getElementById("hint");
const result = document.getElementById("result");
const canvas = document.getElementById("confettiCanvas");
const ctx = canvas.getContext("2d");

let confetti = [];

function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener("resize", resizeCanvas);

noBtn.addEventListener("mouseenter", () => {
  hint.style.display = "block";
  const x = Math.random() * 200 - 100;
  const y = Math.random() * 120 - 60;
  noBtn.style.transform = `translate(${x}px, ${y}px)`;
});

yesBtn.addEventListener("click", () => {
  zone.style.display = "none";
  hint.style.display = "none";
  result.style.display = "block";
  launchConfetti();
});

function launchConfetti() {
  confetti = Array.from({ length: 160 }, () => ({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height - canvas.height,
    r: Math.random() * 6 + 4,
    d: Math.random() * 4 + 2,
    c: ["#7b3fe4", "#b07cff", "#ffffff"][Math.floor(Math.random() * 3)]
  }));
  animateConfetti();
}

function animateConfetti() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  confetti.forEach(p => {
    ctx.beginPath();
    ctx.fillStyle = p.c;
    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
    ctx.fill();
    p.y += p.d;
    if (p.y > canvas.height) p.y = -10;
  });
  requestAnimationFrame(animateConfetti);
}
</script>

</body>
</html>
