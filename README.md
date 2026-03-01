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

/* Main Container */
.container {text-align:center; padding:100px 20px;}
.title {font-size:80px; font-weight:800; position:relative; opacity:0; animation:appearStars 2s forwards; letter-spacing:5px;}
@keyframes appearStars {0%{opacity:0;}50%{opacity:1;}100%{opacity:1;}}
.subtitle {margin-top:20px;font-size:20px;opacity:0;transform:translateX(-100%);animation:slideIn 1.5s forwards;}
.subtitle:nth-child(2){animation-delay:0.5s;}
.subtitle:nth-child(3){animation-delay:0.8s;}
.subtitle:nth-child(4){animation-delay:1.1s;}
@keyframes slideIn {to{opacity:1; transform:translateX(0);}}
.vip-card {margin:80px auto;background:rgba(255,255,255,0.05);padding:40px;width:90%;max-width:400px;border-radius:15px;box-shadow:0 0 30px rgba(0,0,0,0.8);transition:0.4s;backdrop-filter:blur(5px);}
.vip-card:hover{transform:translateY(-10px);box-shadow:0 0 40px rgba(255,255,255,0.2);}
.vip-title{font-family:'Cinzel', serif;font-size:28px;margin-bottom:20px;color:#fff;}
.vip-text{margin:10px 0;opacity:0;transform:translateX(-100%);animation:slideIn 1.5s forwards;color:#eee;}
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
const canvas=document.getElementById("bgCanvas");
const ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;

// Planets
let planets=[];
for(let i=0;i<6;i++){
    planets.push({
        x:Math.random()*canvas.width,
        y:Math.random()*canvas.height/2,
        radius:Math.random()*50+20,
        angle:Math.random()*Math.PI*2,
        speed:0.001 + Math.random()*0.002,
        color:`hsl(${Math.random()*360}, 70%, 50%)`
    });
}

// EMA-like lines
let lines=[];
for(let i=0;i<5;i++){
    let points=[];
    for(let x=0;x<canvas.width;x+=20){
        points.push({x:x, y:canvas.height/2 + Math.sin(x*0.01 + i)*50*Math.random()});
    }
    lines.push({points, color:`hsl(${i*60},80%,60%)`});
}

// Particles - dollar/coins
let particles=[];
function addParticle(){
    particles.push({
        x:Math.random()*canvas.width,
        y:canvas.height,
        size:Math.random()*5+2,
        speedY:Math.random()*2+1,
        speedX:(Math.random()-0.5)*1,
        opacity:Math.random()*0.5+0.5
    });
}

// Animate
function animate(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    
    // Background glow
    let gradient = ctx.createRadialGradient(canvas.width/2, canvas.height/2, 50, canvas.width/2, canvas.height/2, canvas.width);
    gradient.addColorStop(0,"rgba(0,0,0,0.7)");
    gradient.addColorStop(1,"#000");
    ctx.fillStyle=gradient;
    ctx.fillRect(0,0,canvas.width,canvas.height);
    
    // Planets
    planets.forEach(p=>{
        p.angle+=p.speed;
        let px = canvas.width/2 + Math.cos(p.angle)*(p.x-canvas.width/2);
        let py = canvas.height/2 + Math.sin(p.angle)*(p.y-canvas.height/2);
        ctx.beginPath();
        ctx.arc(px, py, p.radius, 0, Math.PI*2);
        ctx.fillStyle=p.color;
        ctx.fill();
    });
    
    // EMA lines
    lines.forEach(line=>{
        ctx.beginPath();
        ctx.moveTo(line.points[0].x, line.points[0].y);
        line.points.forEach(pt=>{
            pt.y += (Math.random()-0.5)*2; // slight fluctuation
            ctx.lineTo(pt.x, pt.y);
        });
        ctx.strokeStyle=line.color;
        ctx.lineWidth=2;
        ctx.stroke();
    });
    
    // Particles
    if(Math.random()<0.3) addParticle();
    particles.forEach((p,i)=>{
        p.y -= p.speedY;
        p.x += p.speedX;
        ctx.fillStyle=`rgba(255,223,0,${p.opacity})`;
        ctx.beginPath();
        ctx.arc(p.x,p.y,p.size,0,Math.PI*2);
        ctx.fill();
        if(p.y<0) particles.splice(i,1);
    });
    
    requestAnimationFrame(animate);
}
animate();

window.addEventListener("resize",()=>{
    canvas.width=window.innerWidth;
    canvas.height=window.innerHeight;
});

function joinVIP(){alert("Welcome to the VIP zone!");}
</script>

</body>
</html>
