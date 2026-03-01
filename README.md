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
.vip-card {margin:80px auto;background:rgba(255,255,255,0.05);padding:40px;width:90%;max-width:400px;border-radius:15px;box-shadow:0 0 30px rgba(0,0,0,0.8);transition:0.4s;backdrop-filter:blur(8px);}
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

/* ===========================
   ANIMATED FRACTAL ENGINE
   =========================== */

let time = 0;

function drawFractal(cx, cy, radius, depth, angleOffset) {
    if (depth === 0) return;

    const branches = 6;
    for (let i = 0; i < branches; i++) {
        const angle = (Math.PI * 2 / branches) * i + angleOffset;
        const x = cx + Math.cos(angle) * radius;
        const y = cy + Math.sin(angle) * radius;

        ctx.beginPath();
        ctx.moveTo(cx, cy);
        ctx.lineTo(x, y);
        ctx.stroke();

        drawFractal(x, y, radius * 0.5, depth - 1, angleOffset + 0.1);
    }
}

function animate() {
    ctx.clearRect(0,0,canvas.width,canvas.height);

    // Dark animated gradient
    let gradient = ctx.createRadialGradient(
        canvas.width/2,
        canvas.height/2,
        0,
        canvas.width/2,
        canvas.height/2,
        canvas.width
    );
    gradient.addColorStop(0,"#0f2027");
    gradient.addColorStop(1,"#000000");
    ctx.fillStyle = gradient;
    ctx.fillRect(0,0,canvas.width,canvas.height);

    ctx.strokeStyle = "rgba(0,255,200,0.25)";
    ctx.lineWidth = 1;

    time += 0.01;

    drawFractal(
        canvas.width/2,
        canvas.height/2,
        120 + Math.sin(time)*30,
        4,
        time
    );

    requestAnimationFrame(animate);
}

animate();

function joinVIP(){ alert("Welcome to the VIP zone!"); }
</script>

</body>
</html>
