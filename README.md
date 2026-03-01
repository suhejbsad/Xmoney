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
  position:relative;
  opacity:0;
  animation:fadeIn 2s forwards;
}
.subtitle {
  margin-top:20px;
  font-size:20px;
  color:white;
  opacity:0;
  transform:translateY(20px);
  animation:slideIn 1.5s forwards;
}
.subtitle:nth-child(2){animation-delay:0.5s;}
.subtitle:nth-child(3){animation-delay:0.8s;}
.subtitle:nth-child(4){animation-delay:1.1s;}
@keyframes fadeIn {0%{opacity:0;}100%{opacity:1;}}
@keyframes slideIn {to{opacity:1; transform:translateY(0);}}

.vip-card {margin:80px auto;background:rgba(0,0,0,0.3);border:2px solid #0ff;padding:40px;width:90%;max-width:400px;border-radius:18px;box-shadow:0 0 30px #0ff;backdrop-filter:blur(12px);transition:0.5s;}
.vip-card:hover {transform:translateY(-8px);box-shadow:0 0 50px #0ff;}
.vip-title {font-family:'Cinzel', serif;font-size:28px;margin-bottom:20px;color:#0ff;}
.vip-text {margin:10px 0;color:#0ff;opacity:0;transform:translateY(20px);animation:slideIn 1.5s forwards;}
.vip-text:nth-child(2){animation-delay:1.2s;}
.vip-text:nth-child(3){animation-delay:1.5s;}
.vip-text:nth-child(4){animation-delay:1.8s;}
.join-btn {margin-top:20px;padding:12px 30px;background:#0ff;border:none;border-radius:8px;color:black;font-size:16px;font-weight:bold;cursor:pointer;transition:0.3s;}
.join-btn:hover {background:white;color:#0ff;}

#memberCounter {
  margin-top:20px;
  font-size:20px;
  color:white;
  text-align:center;
  font-weight:bold;
  text-shadow:none;
}
@media(max-width:768px){
  .title{font-size:120px;}
  .subtitle{font-size:16px;}
  #memberCounter{font-size:16px;}
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
<p class="vip-text">2 - 55% - 60% Guaranteed Win Rate</p>
<p class="vip-text">3 - 3 Signals Per Day (Sometimes More)</p>
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
   ULTRA REALISTIC SHARK INTRO
   ========================= */

let intro = true;
let startTime = null;
let angle = 0;
let zoom = 1;

function drawRealisticShark(cx,cy,scale,open){
  ctx.save();
  ctx.translate(cx,cy);
  ctx.scale(scale,scale);
  ctx.rotate(angle);

  let bodyGrad = ctx.createLinearGradient(-300,-100,300,100);
  bodyGrad.addColorStop(0,"#0a1a22");
  bodyGrad.addColorStop(0.5,"#2f4f5f");
  bodyGrad.addColorStop(1,"#0a1a22");
  ctx.fillStyle = bodyGrad;

  ctx.beginPath();
  ctx.ellipse(0,0,320,90,0,0,Math.PI*2);
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(-50,-90);
  ctx.lineTo(40,-200);
  ctx.lineTo(120,-90);
  ctx.closePath();
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(-280,0);
  ctx.lineTo(-380,-80);
  ctx.lineTo(-350,0);
  ctx.lineTo(-380,80);
  ctx.closePath();
  ctx.fill();

  ctx.fillStyle="white";
  ctx.beginPath();
  ctx.arc(150,-20,12,0,Math.PI*2);
  ctx.fill();

  ctx.fillStyle="black";
  ctx.beginPath();
  ctx.arc(155,-20,6,0,Math.PI*2);
  ctx.fill();

  if(open){
    ctx.fillStyle="black";
    ctx.beginPath();
    ctx.ellipse(300,0,120,70,0,0,Math.PI*2);
    ctx.fill();

    ctx.fillStyle="white";
    for(let i=-50;i<=50;i+=20){
      ctx.beginPath();
      ctx.moveTo(260,i);
      ctx.lineTo(280,i-15);
      ctx.lineTo(300,i);
      ctx.closePath();
      ctx.fill();
    }
  }

  ctx.restore();
}

function sharkIntro(timestamp){
  if(!startTime) startTime=timestamp;
  let elapsed = timestamp-startTime;

  ctx.clearRect(0,0,canvas.width,canvas.height);
  ctx.fillStyle="black";
  ctx.fillRect(0,0,canvas.width,canvas.height);

  if(elapsed<3000){
    angle+=0.3;
    let r = Math.min(canvas.width,canvas.height)/3;
    let x = canvas.width/2 + Math.cos(elapsed*0.01)*r;
    let y = canvas.height/2 + Math.sin(elapsed*0.01)*r;
    drawRealisticShark(x,y,0.6,false);
    requestAnimationFrame(sharkIntro);
  }
  else if(elapsed<4500){
    zoom+=0.05;
    drawRealisticShark(canvas.width/2,canvas.height/2,zoom,true);
    requestAnimationFrame(sharkIntro);
  }
  else{
    intro=false;
    animate();
  }
}

/* =========================
   ORIGINAL NEURAL NETWORK
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
    pulse: Math.random()*Math.PI*2
  });
}

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  const gradient = ctx.createLinearGradient(0,0,0,canvas.height);
  gradient.addColorStop(0,"#050510");
  gradient.addColorStop(1,"#000000");
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
        ctx.lineWidth = 1;
        ctx.beginPath();
        ctx.moveTo(n.x,n.y);
        ctx.lineTo(n2.x,n2.y);
        ctx.stroke();
      }
    }
  }

  nodes.forEach(n=>{
    n.pulse += 0.05;
    let glow = 2 + Math.sin(n.pulse)*1.5;
    ctx.beginPath();
    ctx.arc(n.x,n.y,glow,0,Math.PI*2);
    ctx.fillStyle = "rgba(0,255,255,0.9)";
    ctx.shadowColor = "cyan";
    ctx.shadowBlur = 15;
    ctx.fill();
    ctx.shadowBlur = 0;
  });

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
  } else {
    counterEl.textContent = targetNumber + " Members";
  }
}
requestAnimationFrame(countUp);

function joinVIP(){ alert("Welcome to the VIP zone!"); }
</script>

</body>
</html>
