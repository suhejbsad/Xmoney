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
.container {text-align:center; padding:80px 20px; position:relative; z-index:1;}

/* ==================== Xmoney TITLE ==================== */
.title {
  font-family:'Cinzel', serif;
  font-size:200px;
  color:#0ff;
  text-shadow: 0 0 20px #0ff, 0 0 40px #0ff, 0 0 60px #0ff;
  position:relative;
  opacity:0;
  animation:glowIn 2s forwards;
}
@keyframes glowIn {
  0%{opacity:0; transform:scale(0.5) rotateY(0deg);}
  50%{opacity:1; transform:scale(1.1) rotateY(180deg);}
  100%{opacity:1; transform:scale(1) rotateY(360deg);}
}

/* ==================== SUBTITLE ==================== */
.subtitle { 
  margin-top:20px; 
  font-size:20px; 
  color:#0ff; 
  opacity:0; 
  transform:translateY(20px);
  animation:slideIn 1.5s forwards;
}
.subtitle:nth-child(2){animation-delay:0.5s;}
.subtitle:nth-child(3){animation-delay:0.8s;}
.subtitle:nth-child(4){animation-delay:1.1s;}
@keyframes slideIn {to{opacity:1; transform:translateY(0);}}

/* ==================== VIP CARD ==================== */
.vip-card {
  margin:50px auto;
  background:rgba(0,0,0,0.35);
  border:2px solid #0ff;
  padding:40px;
  width:90%;
  max-width:450px;
  border-radius:18px;
  box-shadow:0 0 40px #0ff;
  backdrop-filter:blur(15px);
  transition:0.5s;
}
.vip-card:hover {transform:translateY(-10px); box-shadow:0 0 60px #0ff;}
.vip-title {font-family:'Cinzel', serif; font-size:30px; margin-bottom:20px; color:#0ff;}
.vip-text {margin:10px 0; color:#0ff; opacity:0; transform:translateY(20px); animation:slideIn 1.5s forwards;}
.vip-text:nth-child(2){animation-delay:1.2s;}
.vip-text:nth-child(3){animation-delay:1.5s;}
.vip-text:nth-child(4){animation-delay:1.8s;}
.vip-text:nth-child(5){animation-delay:2.1s;}
.join-btn {margin-top:20px; padding:14px 32px; background:#0ff; border:none; border-radius:10px; color:black; font-size:16px; font-weight:bold; cursor:pointer; transition:0.3s;}
.join-btn:hover {background:white; color:#0ff;}

/* ==================== MEMBER COUNTER & MENTOR STATS ==================== */
#statsWrapper {
  position:absolute;
  bottom:20px;
  left:50%;
  transform:translateX(-50%);
  display:flex;
  justify-content:space-between;
  width:90%;
  max-width:900px;
}

#memberCounter, #mentorStats {
  font-size:22px;
  font-weight:bold;
  color:white;
  opacity:0;
  animation:slideUp 1.5s forwards;
}
#memberCounter {color:#fff; text-align:right; flex:1;}
#mentorStats {color:#fff; text-align:left; flex:1;}
#mentorStats span {display:block; font-size:18px; margin:5px 0; color:#0ff;}
@keyframes slideUp {to{opacity:1; transform:translateY(0);}}

/* ==================== MEDIA ==================== */
@media(max-width:768px){
  .title{font-size:120px;}
  .subtitle{font-size:16px;}
  #memberCounter, #mentorStats {font-size:16px;}
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
</div>
</div>

<!-- Stats poshtë pllakates -->
<div id="statsWrapper">
  <div id="mentorStats">
    <span id="winRate">Win Rate: 0%</span>
    <span id="winTrade">Win Trade: 0</span>
    <span id="lossTrade">Loss Trade: 0</span>
  </div>
  <div id="memberCounter">0 Members</div>
</div>

<script>
const canvas = document.getElementById("bgCanvas");
const ctx = canvas.getContext("2d");

function resize(){ canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
resize();
window.addEventListener("resize", resize);

// ==================== Neon Fluid Background with LESS LINES ====================
const nodes = [];
const NODE_COUNT = 150;
const MAX_DISTANCE = 100; // paksojm vijat

for(let i=0;i<NODE_COUNT;i++){
  nodes.push({
    x: Math.random()*canvas.width,
    y: Math.random()*canvas.height,
    vx: (Math.random()-0.5)*1.0,
    vy: (Math.random()-0.5)*1.0,
    pulse: Math.random()*Math.PI*2
  });
}

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  const gradient = ctx.createLinearGradient(0,0,0,canvas.height);
  gradient.addColorStop(0,"#000010");
  gradient.addColorStop(1,"#000000");
  ctx.fillStyle = gradient;
  ctx.fillRect(0,0,canvas.width,canvas.height);

  for(let i=0;i<nodes.length;i++){
    let n=nodes[i];
    n.x+=n.vx; n.y+=n.vy;
    if(n.x<0||n.x>canvas.width) n.vx*=-1;
    if(n.y<0||n.y>canvas.height) n.vy*=-1;

    for(let j=i+1;j<nodes.length;j++){
      let n2=nodes[j];
      let dx=n.x-n2.x, dy=n.y-n2.y, dist=Math.sqrt(dx*dx+dy*dy);
      if(dist<MAX_DISTANCE){
        ctx.strokeStyle="rgba(0,255,255,"+(1-dist/MAX_DISTANCE)*0.6+")"; // pakso intensitetin
        ctx.lineWidth=1;
        ctx.beginPath(); ctx.moveTo(n.x,n.y); ctx.lineTo(n2.x,n2.y); ctx.stroke();
      }
    }
  }

  nodes.forEach(n=>{
    n.pulse+=0.07;
    let glow=2+Math.sin(n.pulse)*2;
    ctx.beginPath();
    ctx.arc(n.x,n.y,glow,0,Math.PI*2);
    ctx.fillStyle="rgba(0,255,255,0.9)";
    ctx.shadowColor="cyan";
    ctx.shadowBlur=15;
    ctx.fill();
    ctx.shadowBlur=0;
  });

  requestAnimationFrame(animate);
}
animate();

// ==================== Members Count ====================
const memberEl = document.getElementById("memberCounter");
animateNumber(memberEl,1752," Members");

// ==================== Mentor Stats ====================
animateNumber(document.getElementById("winRate"),57,"%","Win Rate: ");
animateNumber(document.getElementById("winTrade"),3831,"","Win Trade: ");
animateNumber(document.getElementById("lossTrade"),2527,"","Loss Trade: ");

function animateNumber(el,target,suffix="",prefix=""){
  let start=0,duration=4000,startTime=null;
  function step(timestamp){
    if(!startTime) startTime=timestamp;
    let progress=timestamp-startTime;
    let current=Math.min(Math.floor(progress/duration*target),target);
    el.textContent=prefix+current+suffix;
    if(progress<duration) requestAnimationFrame(step);
  }
  requestAnimationFrame(step);
}

function joinVIP(){ alert("Welcome to the VIP zone!"); }
</script>
</body>
</html>
