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

/* ------------------- Xmoney SUPER BOLD ------------------- */
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

/* VIP Card */
.vip-card {margin:80px auto;background:rgba(0,0,0,0.3);border:2px solid #0ff;padding:40px;width:90%;max-width:400px;border-radius:18px;box-shadow:0 0 30px #0ff;backdrop-filter:blur(12px);transition:0.5s;}
.vip-card:hover {transform:translateY(-8px);box-shadow:0 0 50px #0ff;}
.vip-title {font-family:'Cinzel', serif;font-size:28px;margin-bottom:20px;color:#0ff;}
.vip-text {margin:10px 0;color:#0ff;opacity:0;transform:translateY(20px);animation:slideIn 1.5s forwards;}
.vip-text:nth-child(2){animation-delay:1.2s;}
.vip-text:nth-child(3){animation-delay:1.5s;}
.vip-text:nth-child(4){animation-delay:1.8s;}
.join-btn {margin-top:20px;padding:12px 30px;background:#0ff;border:none;border-radius:8px;color:black;font-size:16px;font-weight:bold;cursor:pointer;transition:0.3s;}
.join-btn:hover {background:white;color:#0ff;}
#memberCounter {margin-top:20px; font-size:20px; color:white; text-align:center; font-weight:bold;}
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

<script src="https://cdn.jsdelivr.net/npm/three@0.156.0/build/three.min.js"></script>
<script>
// ---------------- Holographic Grid Background ----------------
const canvas = document.getElementById("bgCanvas");
const renderer = new THREE.WebGLRenderer({canvas: canvas, antialias:true});
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.setPixelRatio(window.devicePixelRatio);

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(60, window.innerWidth/window.innerHeight, 0.1, 1000);
camera.position.set(0,2,5);

// Grid Group
const gridGroup = new THREE.Group();
scene.add(gridGroup);

const gridMaterial = new THREE.LineBasicMaterial({color:0x00ffff, transparent:true, opacity:0.6});
const gridSize = 20;
const gridDivisions = 40;

for(let i=-gridSize;i<=gridSize;i+=gridSize/gridDivisions){
  const geometryX = new THREE.BufferGeometry().setFromPoints([new THREE.Vector3(-gridSize,0,i), new THREE.Vector3(gridSize,0,i)]);
  const geometryZ = new THREE.BufferGeometry().setFromPoints([new THREE.Vector3(i,0,-gridSize), new THREE.Vector3(i,0,gridSize)]);
  gridGroup.add(new THREE.Line(geometryX, gridMaterial));
  gridGroup.add(new THREE.Line(geometryZ, gridMaterial));
}

// Floating points above grid
const pointGeometry = new THREE.SphereGeometry(0.05,8,8);
const pointMaterial = new THREE.MeshBasicMaterial({color:0x00ffff});
const points = [];
for(let i=0;i<150;i++){
  const point = new THREE.Mesh(pointGeometry, pointMaterial);
  point.position.set((Math.random()-0.5)*gridSize*2, Math.random()*2, (Math.random()-0.5)*gridSize*2);
  scene.add(point);
  points.push(point);
}

function animate(){
  requestAnimationFrame(animate);
  const time = performance.now() * 0.001;

  // Rotate grid slowly
  gridGroup.rotation.y = time * 0.05;
  gridGroup.rotation.x = Math.sin(time*0.2)*0.05;

  // Make points pulse
  points.forEach(p=>{
    p.position.y = Math.sin(time + p.position.x + p.position.z)*0.5 + 1;
  });

  renderer.render(scene,camera);
}
animate();

window.addEventListener("resize", ()=>{
  renderer.setSize(window.innerWidth, window.innerHeight);
  camera.aspect = window.innerWidth/window.innerHeight;
  camera.updateProjectionMatrix();
});

// ---------------- MEMBER COUNTER ----------------
const counterEl = document.getElementById("memberCounter");
const targetNumber = 1752;
const duration = 4000;
let startTime = null;

function countUp(timestamp){
  if(!startTime) startTime = timestamp;
  let progress = timestamp - startTime;
  let current = Math.min(Math.floor((progress/duration)*targetNumber), targetNumber);
  counterEl.textContent = current + " Members";
  if(progress < duration) requestAnimationFrame(countUp);
}
requestAnimationFrame(countUp);

function joinVIP(){ alert("Welcome to the VIP zone!"); }
</script>

</body>
</html>
