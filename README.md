<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Xmoney</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600;800&family=Cinzel:wght@600&display=swap" rel="stylesheet">
<style>
* {margin:0; padding:0; box-sizing:border-box; font-family:'Poppins',sans-serif;}
body {background:#000; color:white; overflow:hidden;}
canvas {position:fixed; top:0; left:0; width:100%; height:100%; z-index:-1;}
.container {text-align:center; padding:100px 20px; position:relative; z-index:1;}

.title {
  font-family:'Cinzel', serif;
  font-size:240px;
  color:white;
  letter-spacing:5px;
  opacity:0;
  animation:fadeIn 2s forwards;
  animation-delay:3.2s;
}
.subtitle {
  margin-top:20px;
  font-size:20px;
  color:white;
  opacity:0;
  transform:translateY(20px);
  animation:slideIn 1.5s forwards;
  animation-delay:3.5s;
}
.subtitle:nth-of-type(2){animation-delay:3.8s;}
.subtitle:nth-of-type(3){animation-delay:4.1s;}

@keyframes fadeIn {to{opacity:1;}}
@keyframes slideIn {to{opacity:1; transform:translateY(0);}}

.vip-card {
  margin:80px auto;
  background:rgba(0,0,0,0.3);
  border:2px solid #0ff;
  padding:40px;
  width:90%;
  max-width:400px;
  border-radius:18px;
  box-shadow:0 0 30px #0ff;
  backdrop-filter:blur(12px);
  transition:0.5s;
  opacity:0;
  animation:fadeIn 2s forwards;
  animation-delay:4.5s;
}
.vip-card:hover {transform:translateY(-8px);box-shadow:0 0 50px #0ff;}
.vip-title {font-family:'Cinzel', serif;font-size:28px;margin-bottom:20px;color:#0ff;}
.vip-text {margin:10px 0;color:#0ff;}
.join-btn {
  margin-top:20px;
  padding:12px 30px;
  background:#0ff;
  border:none;
  border-radius:8px;
  color:black;
  font-size:16px;
  font-weight:bold;
  cursor:pointer;
  transition:0.3s;
}
.join-btn:hover {background:white;color:#0ff;}

#memberCounter {
  margin-top:20px;
  font-size:20px;
  font-weight:bold;
}

@media(max-width:768px){
  .title{font-size:120px;}
  .subtitle{font-size:16px;}
}
</style>
</head>
<body>

<canvas id="bgCanvas"></canvas>

<div class="container">
<h1 class="title">Xmoney</h1>
<p class="subtitle">The Billionaire Circle</p>
<p class="subtitle">We Print Money Like a Factory</p>
<p class="subtitle">Forex Is Our Game</p>

<div class="vip-card">
<h2 class="vip-title">VIP ZONE</h2>
<p class="vip-text">1 - Daily Forex Signals</p>
<p class="vip-text">2 - 55% - 60% Win Rate</p>
<p class="vip-text">3 - 3 Signals Per Day</p>
<button class="join-btn" onclick="joinVIP()">JOIN</button>
<div id="memberCounter">0 Members</div>
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

/* =========================
   GIANT SHARK FROM DARKNESS
   ========================= */

let introStart = null;
let sharkScale = 0.3;
let sharkAlpha = 0;
let attackZoom = 1;

function drawDarkShark(cx, cy, scale, alpha, attack=false){
  ctx.save();
  ctx.globalAlpha = alpha;
  ctx.translate(cx, cy);
  ctx.scale(scale, scale);

  let bodyGrad = ctx.createLinearGradient(-400,-200,400,200);
  bodyGrad.addColorStop(0,"#000");
  bodyGrad.addColorStop(0.5,"#1a2a33");
  bodyGrad.addColorStop(1,"#000");
  ctx.fillStyle = bodyGrad;

  ctx.beginPath();
  ctx.ellipse(0,0,420,120,0,0,Math.PI*2);
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(-40,-120);
  ctx.lineTo(80,-260);
  ctx.lineTo(160,-120);
  ctx.closePath();
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(-380,0);
  ctx.lineTo(-520,-120);
  ctx.lineTo(-480,0);
  ctx.lineTo(-520,120);
  ctx.closePath();
  ctx.fill();

  ctx.shadowColor="#00eaff";
  ctx.shadowBlur=40;
  ctx.fillStyle="#00eaff";
  ctx.beginPath();
  ctx.arc(200,-30,18,0,Math.PI*2);
  ctx.fill();
  ctx.shadowBlur=0;

  if(attack){
    ctx.fillStyle="black";
    ctx.beginPath();
    ctx.ellipse(380,20,200,120,0,0,Math.PI*2);
    ctx.fill();

    ctx.fillStyle="white";
    for(let i=-80;i<=80;i+=25){
      ctx.beginPath();
      ctx.moveTo(330,i);
      ctx.lineTo(360,i-25);
      ctx.lineTo(390,i);
      ctx.closePath();
      ctx.fill();
    }
  }

  ctx.restore();
}

function sharkIntro(timestamp){
  if(!introStart) introStart = timestamp;
  let elapsed = timestamp - introStart;

  ctx.clearRect(0,0,canvas.width,canvas.height);
  ctx.fillStyle="black";
  ctx.fillRect(0,0,canvas.width,canvas.height);

  if(elapsed < 1200){
    sharkAlpha += 0.02;
    drawDarkShark(canvas.width/2,canvas.height/2,sharkScale,sharkAlpha,false);
  }
  else if(elapsed < 2200){
    sharkScale += 0.01;
    sharkAlpha += 0.02;
    drawDarkShark(canvas.width/2,canvas.height/2,sharkScale,sharkAlpha,false);
  }
  else if(elapsed < 3000){
    attackZoom += 0.08;
    let shakeX = (Math.random()-0.5)*15;
    let shakeY = (Math.random()-0.5)*15;
    drawDarkShark(
      canvas.width/2 + shakeX,
      canvas.height/2 + shakeY,
      sharkScale * attackZoom,
      1,
      true
    );
  }
  else if(elapsed < 3300){
    ctx.fillStyle="white";
    ctx.fillRect(0,0,canvas.width,canvas.height);
  }
  else{
    animate();
    return;
  }

  requestAnimationFrame(sharkIntro);
}

/* =========================
   NEURAL NETWORK BACKGROUND
   ========================= */

const nodes = [];
const NODE_COUNT = 120;
const MAX_DISTANCE = 150;

for(let i=0;i<NODE_COUNT;i++){
  nodes.push({
    x: Math.random()*canvas.width,
    y: Math.random()*canvas.height,
    vx: (Math.random()-0.5)*0.7,
    vy: (Math.random()-0.5)*0.7,
  });
}

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  const gradient = ctx.createLinearGradient(0,0,0,canvas.height);
  gradient.addColorStop(0,"#050510");
  gradient.addColorStop(1,"#000");
  ctx.fillStyle = gradient;
  ctx.fillRect(0,0,canvas.width,canvas.height);

  for(let i=0;i<nodes.length;i++){
    let n = nodes[i];
    n.x += n.vx;
    n.y += n.vy;
    if(n.x<0||n.x>canvas.width) n.vx*=-1;
    if(n.y<0||n.y>canvas.height) n.vy*=-1;

    for(let j=i+1;j<nodes.length;j++){
      let n2 = nodes[j];
      let dx = n.x - n2.x;
      let dy = n.y - n2.y;
      let dist = Math.sqrt(dx*dx+dy*dy);
      if(dist < MAX_DISTANCE){
        ctx.strokeStyle = "rgba(0,200,255,"+(1-dist/MAX_DISTANCE)+")";
        ctx.beginPath();
        ctx.moveTo(n.x,n.y);
        ctx.lineTo(n2.x,n2.y);
        ctx.stroke();
      }
    }

    ctx.beginPath();
    ctx.arc(n.x,n.y,2,0,Math.PI*2);
    ctx.fillStyle = "cyan";
    ctx.fill();
  }

  requestAnimationFrame(animate);
}

requestAnimationFrame(sharkIntro);

/* COUNTER */
const counterEl = document.getElementById("memberCounter");
const targetNumber = 1752;
const duration = 4000;
let counterStart = null;

function countUp(timestamp){
  if(!counterStart) counterStart = timestamp;
  let progress = timestamp - counterStart;
  let current = Math.min(Math.floor((progress/duration)*targetNumber), targetNumber);
  counterEl.textContent = current + " Members";
  if(progress < duration){
    requestAnimationFrame(countUp);
  }
}
requestAnimationFrame(countUp);

function joinVIP(){ alert("Welcome to the VIP zone!"); }
</script>

</body>
</html>
