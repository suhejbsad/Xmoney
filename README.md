<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Xmoney</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600;800&family=Cinzel:wght@600&display=swap" rel="stylesheet">
<style>

* {
margin: 0;
padding: 0;
box-sizing: border-box;
font-family: 'Poppins', sans-serif;
}

body {
background: #000;
color: white;
overflow-x: hidden;
}

/* Background Chart */
canvas {
position: fixed;
top: 0;
left: 0;
width: 100%;
height: 100%;
z-index: -1;
filter: blur(2px);
opacity: 0.9;
}

/* Main Container */
.container {
text-align: center;
padding: 100px 20px;
}

/* Xmoney Title */
.title {
font-size: 60px;
font-weight: 800;
position: relative;
opacity: 0;
transform: translateX(-100%);
animation: slideIn 1.5s forwards;
}

/* Shine Effect */
.title::after {
content: '';
position: absolute;
top: 0;
left: -100%;
width: 50%;
height: 100%;
background: linear-gradient(120deg, transparent, rgba(255,255,255,0.8), transparent);
animation: shine 3s infinite;
}

@keyframes shine {
0% { left: -100%; }
50% { left: 120%; }
100% { left: 120%; }
}

/* Subtitle */
.subtitle {
margin-top: 20px;
font-size: 20px;
opacity: 0;
transform: translateX(-100%);
animation: slideIn 1.5s forwards;
}

.subtitle:nth-child(2) { animation-delay: 0.5s; }
.subtitle:nth-child(3) { animation-delay: 0.8s; }
.subtitle:nth-child(4) { animation-delay: 1.1s; }

@keyframes slideIn {
to {
opacity: 1;
transform: translateX(0);
}
}

/* VIP Card */
.vip-card {
margin: 80px auto;
background: rgba(0,0,0,0.8);
padding: 40px;
width: 90%;
max-width: 400px;
border-radius: 15px;
box-shadow: 0 0 30px rgba(0,0,0,0.8);
transition: 0.4s;
}

.vip-card:hover {
transform: translateY(-10px);
box-shadow: 0 0 40px gold;
}

.vip-title {
font-family: 'Cinzel', serif;
font-size: 28px;
margin-bottom: 20px;
}

.vip-text {
margin: 10px 0;
opacity: 0;
transform: translateX(-100%);
animation: slideIn 1.5s forwards;
}

.vip-text:nth-child(2) { animation-delay: 1.2s; }
.vip-text:nth-child(3) { animation-delay: 1.5s; }
.vip-text:nth-child(4) { animation-delay: 1.8s; }

.join-btn {
margin-top: 20px;
padding: 12px 30px;
background: gray;
border: none;
border-radius: 8px;
color: white;
font-size: 16px;
cursor: pointer;
transition: 0.3s;
}

.join-btn:hover {
background: gold;
color: black;
}

/* Responsive */
@media(max-width:768px){
.title { font-size: 40px; }
.subtitle { font-size: 16px; }
}

</style>
</head>
<body>

<canvas id="chart"></canvas>

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
const canvas = document.getElementById("chart");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let candles = [];
let offset = 0;

// Gjenero candles me lartësi dhe wicks
function generateCandles(){
    candles = [];
    let base = canvas.height / 2;

    for(let i=0; i<150; i++){
        let open = base + (Math.random() - 0.5) * 200;
        let close = open + (Math.random() - 0.5) * 150;
        let high = Math.max(open, close) + Math.random() * 80;
        let low = Math.min(open, close) - Math.random() * 80;

        candles.push({ x: i * 20, open, close, high, low });
    }
}

// Draw grid Forex-style
function drawGrid(){
    ctx.strokeStyle = "rgba(255,215,0,0.08)";
    ctx.lineWidth = 1;

    for(let i=0; i<canvas.width; i+=80){
        ctx.beginPath();
        ctx.moveTo(i - offset % 80, 0);
        ctx.lineTo(i - offset % 80, canvas.height);
        ctx.stroke();
    }

    for(let j=0; j<canvas.height; j+=80){
        ctx.beginPath();
        ctx.moveTo(0, j);
        ctx.lineTo(canvas.width, j);
        ctx.stroke();
    }
}

// Draw candles
function drawCandles(){
    candles.forEach(c=>{
        let x = c.x - offset;

        // Vetka (wick)
        ctx.strokeStyle = "rgba(255,215,0,0.6)";
        ctx.beginPath();
        ctx.moveTo(x + 5, c.high);
        ctx.lineTo(x + 5, c.low);
        ctx.stroke();

        // Body
        if(c.close > c.open){
            ctx.fillStyle = "gold";
            ctx.fillRect(x, c.open, 10, c.close - c.open);
        } else {
            ctx.fillStyle = "white";
            ctx.fillRect(x, c.close, 10, c.open - c.close);
        }
    });
}

// Animacion lëvizëse
function animate(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    drawGrid();
    drawCandles();

    offset += 1;
    if(offset > candles.length * 20){
        generateCandles();
        offset = 0;
    }

    requestAnimationFrame(animate);
}

generateCandles();
animate();

// Resize i responsive
window.addEventListener("resize", ()=>{
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    generateCandles();
});

// Placeholder për button JOIN
function joinVIP(){
    alert("Welcome to the VIP zone!");
}
</script>

</body>
</html>
