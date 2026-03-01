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
.container {text-align:center; padding:100px 20px; position:relative; z-index:1; opacity:0; transition:opacity 1s ease;}

/* ------------------- Xmoney SUPER BOLD ------------------- */
.title {
  font-family:'Cinzel', serif;
  font-size:240px;
  color:white;
  letter-spacing:5px;
  position:relative;
  opacity:0;
  animation:fadeIn 2s forwards 0.2s;
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

/* COUNTER */
#memberCounter {margin-top:20px;font-size:20px;color:white;text-align:center;font-weight:bold;text-shadow:none;}
@media(max-width:768px){.title{font-size:120px;}.subtitle{font-size:16px;}#memberCounter{font-size:16px;}}
</style>
</head>
<body>

<canvas id="bgCanvas"></canvas>

<div class="container" id="mainContent">
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
// ------------------ Fluidic Intro 3D ------------------
let scene = new THREE.Scene();
let camera = new THREE.PerspectiveCamera(60, window.innerWidth/window.innerHeight, 0.1, 1000);
camera.position.z = 3;

let renderer = new THREE.WebGLRenderer({canvas:document.getElementById('bgCanvas'), antialias:true});
renderer.setSize(window.innerWidth, window.innerHeight);

// Plane with Shader Material
let uniforms = {
  u_time: {value: 0},
  u_resolution: {value: new THREE.Vector2(window.innerWidth, window.innerHeight)}
};

let material = new THREE.ShaderMaterial({
  uniforms: uniforms,
  vertexShader: `
    varying vec2 vUv;
    void main(){
      vUv = uv;
      gl_Position = projectionMatrix * modelViewMatrix * vec4(position,1.0);
    }
  `,
  fragmentShader: `
    uniform float u_time;
    uniform vec2 u_resolution;
    varying vec2 vUv;
    
    void main(){
      vec2 uv = vUv - 0.5;
      float r = length(uv);
      float angle = atan(uv.y, uv.x);
      
      float wave = sin(10.0*r - u_time*5.0 + angle*5.0);
      float glow = smoothstep(0.4,0.0,wave);
      
      vec3 color = mix(vec3(0.0,0.05,0.2), vec3(0.0,0.7,1.0), glow);
      gl_FragColor = vec4(color,1.0);
    }
  `
});

let geometry = new THREE.PlaneGeometry(5,5,32,32);
let plane = new THREE.Mesh(geometry, material);
scene.add(plane);

window.addEventListener("resize",()=>{
  renderer.setSize(window.innerWidth, window.innerHeight);
  camera.aspect = window.innerWidth/window.innerHeight;
  camera.updateProjectionMatrix();
  uniforms.u_resolution.value.set(window.innerWidth, window.innerHeight);
});

// Animate Intro
let introDuration = 3000; // 3 sekonda
let startTime = performance.now();

function animateIntro(time){
  let elapsed = time - startTime;
  uniforms.u_time.value = elapsed * 0.002; // scale time

  renderer.render(scene, camera);
  
  if(elapsed < introDuration){
    requestAnimationFrame(animateIntro);
  } else {
    // Fade out fluidic intro
    plane.material.transparent = true;
    let fade = {opacity:1};
    let fadeInterval = setInterval(()=>{
      fade.opacity -= 0.03;
      plane.material.opacity = fade.opacity;
      if(fade.opacity <= 0){
        clearInterval(fadeInterval);
        document.getElementById('mainContent').style.opacity = 1; // show content
      }
    },16);
  }
}
requestAnimationFrame(animateIntro);

// ------------------ Member Counter ------------------
const counterEl = document.getElementById("memberCounter");
const targetNumber = 1752;
const duration = 4000;
let counterStart = null;
function countUp(timestamp){
  if(!counterStart) counterStart = timestamp;
  let progress = timestamp - counterStart;
  let current = Math.min(Math.floor((progress/duration)*targetNumber), targetNumber);
  counterEl.textContent = current + " Members";
  if(progress < duration) requestAnimationFrame(countUp);
}
requestAnimationFrame(countUp);

function joinVIP(){ alert("Welcome to the VIP zone!"); }
</script>
</body>
</html>
