<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Xmoney | The Billionaire Circle</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600;800&family=Cinzel:wght@600;900&display=swap" rel="stylesheet">
<style>
/* --- BASE STYLES --- */
* {margin:0; padding:0; box-sizing:border-box; font-family:'Poppins',sans-serif;}
body {
    background: #000; 
    color: white; 
    overflow-x: hidden; 
    min-height: 100vh;
}
canvas {position:fixed; top:0; left:0; width:100%; height:100%; z-index:-1;}

/* --- BACKGROUND GLOWS --- */
.glow-bg {
    position: fixed;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(0, 255, 255, 0.1) 0%, transparent 70%);
    z-index: -1;
    filter: blur(80px);
}

.container {text-align:center; padding:80px 20px; position:relative; z-index:1;}

/* --- Xmoney SUPER BOLD (UPGRADED) --- */
.title {
  font-family:'Cinzel', serif;
  font-size: clamp(80px, 20vw, 240px); /* Responsive sizing */
  font-weight: 900;
  color: white;
  letter-spacing: 10px;
  position: relative;
  opacity: 0;
  animation: fadeIn 2s forwards;
  text-shadow: 0 0 30px rgba(0, 255, 255, 0.3);
}

.subtitle-container { margin-bottom: 50px; }
.subtitle {
  margin-top: 10px;
  font-size: 22px;
  color: #aaa;
  letter-spacing: 3px;
  text-transform: uppercase;
  opacity: 0;
  transform: translateY(20px);
  animation: slideIn 1.5s forwards;
}
.subtitle:nth-child(2){animation-delay:0.5s;}
.subtitle:nth-child(3){animation-delay:0.8s;}
.subtitle:nth-child(4){animation-delay:1.1s;}

/* --- VIP CARD - HIGH END OVERHAUL --- */
.vip-card {
    margin: 40px auto;
    position: relative;
    padding: 3px; /* Space for the animated border */
    width: 95%;
    max-width: 450px;
    background: linear-gradient(135deg, #0ff, #005555);
    border-radius: 24px;
    overflow: hidden;
    transition: 0.5s;
}

.vip-inner {
    background: rgba(0, 5, 10, 0.95);
    padding: 50px 40px;
    border-radius: 22px;
    backdrop-filter: blur(20px);
}

.vip-card:hover {
    transform: scale(1.03) translateY(-10px);
    box-shadow: 0 0 60px rgba(0, 255, 255, 0.4);
}

.vip-title {
    font-family:'Cinzel', serif;
    font-size: 32px;
    margin-bottom: 25px;
    color: #0ff;
    letter-spacing: 4px;
    text-shadow: 0 0 10px #0ff;
}

.vip-text {
    margin: 15px 0;
    font-size: 18px;
    color: #e0faff;
    font-weight: 300;
    opacity: 0;
    transform: translateX(-20px);
    animation: slideRight 1s forwards;
}
.vip-text:nth-child(2){animation-delay:1.5s;}
.vip-text:nth-child(3){animation-delay:1.8s;}
.vip-text:nth-child(4){animation-delay:2.1s;}

.join-btn {
    margin-top: 30px;
    padding: 15px 50px;
    background: #0ff;
    border: none;
    border-radius: 50px;
    color: black;
    font-size: 18px;
    font-weight: 800;
    text-transform: uppercase;
    cursor: pointer;
    transition: 0.3s;
    box-shadow: 0 5px 15px rgba(0, 255, 255, 0.4);
}

.join-btn:hover {
    background: white;
    transform: letter-spacing 0.2s;
    letter-spacing: 2px;
}

/* --- COUNTER --- */
#memberCounter {
  margin-top: 30px;
  font-size: 22px;
  color: #0ff;
  font-weight: 800;
  font-family: 'Cinzel', serif;
}

/* --- ANIMATIONS --- */
@keyframes fadeIn { 0%{opacity:0; filter:blur(10px);} 100%{opacity:1; filter:blur(0);} }
@keyframes slideIn { to{opacity:1; transform:translateY(0);} }
@keyframes slideRight { to{opacity:1; transform:translateX(0);} }

@media(max-width:768px){
  .title{font-size:70px; letter-spacing: 2px;}
  .subtitle{font-size:14px;}
  .vip-inner {padding: 30px 20px;}
}
</style>
</head>
<body>

<div class="glow-bg"></div>
<canvas id="bgCanvas"></canvas>

<div class="container">
    <h1 class="title">Xmoney</h1>
    <div class="subtitle-container">
        <p class="subtitle">The Billionaire Circle</p>
        <p class="subtitle">We Print Money Like a Factory</p>
        <p class="subtitle">Forex Is Our Game</p>
    </div>

    <div class="vip-card">
        <div class="vip-inner">
            <h2 class="vip-title">VIP ZONE</h2>
            <p class="vip-text">⚡ 1 - Daily Forex Signals</p>
            <p class="vip-text">📈 2 - 57% - 60% Guaranteed Win Rate</p>
            <p class="vip-text">🔔 3 - 3 Signals Per Day (Sometimes More)</p>
            
            <button class="join-btn" onclick="joinVIP()">JOIN NOW</button>

            <div id="memberCounter">0 Members</div>
        </div>
    </div>
</div>

<script>
const canvas = document.getElementById("bgCanvas");
const ctx = canvas.getContext("2d");

function resize(){
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resize();
window.addEventListener("resize", resize);

const nodes = [];
const mouse = { x: null, y: null };

window.addEventListener('mousemove', (e) => {
    mouse.x = e.x;
    mouse.y = e.y;
});

for(let i=0;i<120;i++){
  nodes.push({
    x: Math.random()*canvas.width,
    y: Math.random()*canvas.height,
    vx: (Math.random()-0.5)*1.2,
    vy: (Math.random()-0.5)*1.2,
    size: Math.random()*2 + 1
  });
}

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  
  // Background gradient depth
  ctx.fillStyle = "rgba(0,0,0,0.2)";
  ctx.fillRect(0,0,canvas.width,canvas.height);

  for(let i=0;i<nodes.length;i++){
    let n = nodes[i];
    n.x += n.vx;
    n.y += n.vy;

    if(n.x<0||n.x>canvas.width) n.vx*=-1;
    if(n.y<0||n.y>canvas.height) n.vy*=-1;

    // Subtle interaction with mouse
    let dx = mouse.x - n.x;
    let dy = mouse.y - n.y;
    let distMouse = Math.sqrt(dx*dx + dy*dy);
    if(distMouse < 150) {
        n.x -= dx/80;
        n.y -= dy/80;
    }

    for(let j=i+1;j<nodes.length;j++){
      let n2 = nodes[j];
      let dx2 = n.x - n2.x;
      let dy2 = n.y - n2.y;
      let dist = Math.sqrt(dx2*dx2+dy2*dy2);
      if(dist < 150){
        ctx.strokeStyle = "rgba(0,255,255,"+(1-dist/150)*0.4+")";
        ctx.lineWidth = 0.5;
        ctx.beginPath();
        ctx.moveTo(n.x,n.y);
        ctx.lineTo(n2.x,n2.y);
        ctx.stroke();
      }
    }
    
    ctx.fillStyle = "#0ff";
    ctx.shadowColor = "#0ff";
    ctx.shadowBlur = 5;
    ctx.beginPath();
    ctx.arc(n.x, n.y, n.size, 0, Math.PI*2);
    ctx.fill();
    ctx.shadowBlur = 0;
  }
  requestAnimationFrame(animate);
}

// COUNTER 0 → 1752
const counterEl = document.getElementById("memberCounter");
const targetNumber = 1752;
const duration = 4000;
let startTime = null;

function countUp(timestamp){
  if(!startTime) startTime = timestamp;
  let progress = timestamp - startTime;
  let current = Math.min(Math.floor((progress/duration)*targetNumber), targetNumber);
  counterEl.textContent = current.toLocaleString() + " Members";
  if(progress < duration) requestAnimationFrame(countUp);
}

requestAnimationFrame(countUp);

function joinVIP(){ 
    const btn = document.querySelector('.join-btn');
    btn.innerHTML = "REDIRECTING...";
    setTimeout(() => {
        alert("Welcome to the Billionaire Circle. Prepare for takeoff.");
        btn.innerHTML = "JOIN NOW";
    }, 800);
}

animate();
</script>
</body>
</html>
