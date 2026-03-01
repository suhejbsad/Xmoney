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
   3D CRYSTAL WHALES ENGINE
   ========================= */

class CrystalWhale {
  constructor(x,y,scale,dir){
    this.x=x;
    this.y=y;
    this.scale=scale;
    this.dir=dir;
    this.angle=0;
    this.depth=Math.random()*0.5+0.5;
  }

  draw(){
    ctx.save();
    ctx.translate(this.x,this.y);
    ctx.scale(this.scale*this.depth,this.scale*this.depth);
    ctx.rotate(Math.sin(this.angle)*0.1);

    let glow = 20 + Math.sin(this.angle*2)*15;

    ctx.shadowColor = "cyan";
    ctx.shadowBlur = glow;

    let gradient = ctx.createLinearGradient(-100,0,100,0);
    gradient.addColorStop(0,"rgba(0,255,255,0.2)");
    gradient.addColorStop(0.5,"rgba(0,255,255,0.9)");
    gradient.addColorStop(1,"rgba(0,255,255,0.2)");

    ctx.fillStyle = gradient;

    ctx.beginPath();
    ctx.moveTo(-120,0);
    ctx.lineTo(-60,-25);
    ctx.lineTo(40,-35);
    ctx.lineTo(120,0);
    ctx.lineTo(40,35);
    ctx.lineTo(-60,25);
    ctx.closePath();
    ctx.fill();

    ctx.shadowBlur = 0;
    ctx.restore();
  }

  update(){
    this.angle += 0.01;
    this.x += this.dir * 0.3 * this.depth;
    this.y += Math.sin(this.angle)*0.2;

    if(this.dir>0 && this.x > canvas.width+200) this.x=-200;
    if(this.dir<0 && this.x < -200) this.x=canvas.width+200;
  }
}

const whales = [
  new CrystalWhale(canvas.width/2, canvas.height*0.25, 1.2, 0.2),  // lart
  new CrystalWhale(-200, canvas.height*0.6, 1, 1),                 // majtas
  new CrystalWhale(canvas.width+200, canvas.height*0.75, 1.1, -1)  // djathtas
];

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  let ocean = ctx.createLinearGradient(0,0,0,canvas.height);
  ocean.addColorStop(0,"#00111a");
  ocean.addColorStop(1,"#000000");
  ctx.fillStyle=ocean;
  ctx.fillRect(0,0,canvas.width,canvas.height);

  whales.forEach(w=>{
    w.update();
    w.draw();
  });

  requestAnimationFrame(animate);
}

/* =========================
   MEMBER COUNTER
   ========================= */

const counterEl = document.getElementById("memberCounter");
const targetNumber = 1752;
const duration = 4000;
let startTime = null;

function countUp(timestamp){
  if(!startTime) startTime = timestamp;
  let progress = timestamp - startTime;
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
animate();
</script>

</body>
</html>
