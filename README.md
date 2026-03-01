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
.container {text-align:center; padding:100px 20px;}
.title {font-size:80px; font-weight:800; position:relative; opacity:0; animation:fadeIn 2s forwards; letter-spacing:5px;}
@keyframes fadeIn {0%{opacity:0;}100%{opacity:1;}}
.subtitle {margin-top:20px;font-size:20px;opacity:0;transform:translateY(20px);animation:slideIn 1.5s forwards;}
.subtitle:nth-child(2){animation-delay:0.5s;}
.subtitle:nth-child(3){animation-delay:0.8s;}
.subtitle:nth-child(4){animation-delay:1.1s;}
@keyframes slideIn {to{opacity:1; transform:translateY(0);}}
.vip-card {margin:80px auto;background:rgba(255,255,255,0.05);padding:40px;width:90%;max-width:400px;border-radius:15px;box-shadow:0 0 30px rgba(0,0,0,0.8);transition:0.4s;backdrop-filter:blur(5px);}
.vip-card:hover{transform:translateY(-10px);box-shadow:0 0 40px rgba(255,255,255,0.2);}
.vip-title{font-family:'Cinzel', serif;font-size:28px;margin-bottom:20px;color:#fff;}
.vip-text{margin:10px 0;opacity:0;transform:translateY(20px);animation:slideIn 1.5s forwards;color:#eee;}
.vip-text:nth-child(2){animation-delay:1.2s;}
.vip-text:nth-child(3){animation-delay:1.5s;}
.vip-text:nth-child(4){animation-delay:1.8s;}
.join-btn{margin-top:20px;padding:12px 30px;background:gray;border:none;border-radius:8px;color:white;font-size:16px;cursor:pointer;transition:0.3s;}
.join-btn:hover{background:white;color:black;}
@media(max-width:768px){.title{font-size:50px;} .subtitle{font-size:16px;}}
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

<script>
const canvas = document.getElementById("bgCanvas");
const ctx = canvas.getContext("2d");

function resizeCanvas(){
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener("resize", resizeCanvas);

/* ===============================
   ULTRA REALISTIC 4K SPACE ENGINE
   =============================== */

let stars = [];
let nebulaParticles = [];
let time = 0;

for(let i=0;i<600;i++){
    stars.push({
        x:Math.random()*canvas.width,
        y:Math.random()*canvas.height,
        size:Math.random()*1.5,
        speed:Math.random()*0.3 + 0.05
    });
}

for(let i=0;i<120;i++){
    nebulaParticles.push({
        x:Math.random()*canvas.width,
        y:Math.random()*canvas.height,
        radius:Math.random()*400 + 200,
        hue:200 + Math.random()*80,
        alpha:Math.random()*0.08
    });
}

function drawDeepSpaceGradient(){
    let gradient = ctx.createRadialGradient(
        canvas.width/2,
        canvas.height/2,
        0,
        canvas.width/2,
        canvas.height/2,
        canvas.width
    );

    gradient.addColorStop(0,"#05070d");
    gradient.addColorStop(0.4,"#0b1320");
    gradient.addColorStop(0.7,"#090a14");
    gradient.addColorStop(1,"#000000");

    ctx.fillStyle = gradient;
    ctx.fillRect(0,0,canvas.width,canvas.height);
}

function drawNebula(){
    nebulaParticles.forEach(p=>{
        let gradient = ctx.createRadialGradient(
            p.x + Math.sin(time*0.0002)*200,
            p.y + Math.cos(time*0.00015)*200,
            0,
            p.x,
            p.y,
            p.radius
        );

        gradient.addColorStop(0,`hsla(${p.hue},100%,60%,${p.alpha})`);
        gradient.addColorStop(1,"transparent");

        ctx.fillStyle = gradient;
        ctx.beginPath();
        ctx.arc(p.x,p.y,p.radius,0,Math.PI*2);
        ctx.fill();
    });
}

function drawStars(){
    stars.forEach(s=>{
        s.y -= s.speed;
        if(s.y < 0){
            s.y = canvas.height;
            s.x = Math.random()*canvas.width;
        }

        ctx.beginPath();
        ctx.fillStyle="white";
        ctx.shadowColor="white";
        ctx.shadowBlur=8;
        ctx.arc(s.x,s.y,s.size,0,Math.PI*2);
        ctx.fill();
        ctx.shadowBlur=0;
    });
}

function animate(){
    time += 1;
    drawDeepSpaceGradient();
    drawNebula();
    drawStars();
    requestAnimationFrame(animate);
}

animate();

function joinVIP(){ alert("Welcome to the VIP zone!"); }
</script>

</body>
</html>
