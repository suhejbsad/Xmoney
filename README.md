<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Xmoney</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600;800&family=Cinzel:wght@600&display=swap" rel="stylesheet">

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins',sans-serif;}
body{background:black;color:white;overflow:hidden;}
#bgCanvas{position:fixed;top:0;left:0;width:100%;height:100%;z-index:-1;}
.container{text-align:center;padding:100px 20px;position:relative;z-index:2;}

.title{
font-family:'Cinzel',serif;
font-size:240px;
letter-spacing:5px;
opacity:0;
animation:fadeIn 2s forwards;
animation-delay:3.2s;
}

.subtitle{
margin-top:20px;
font-size:20px;
opacity:0;
transform:translateY(20px);
animation:slideIn 1.5s forwards;
animation-delay:3.5s;
}

.subtitle:nth-of-type(2){animation-delay:3.8s;}
.subtitle:nth-of-type(3){animation-delay:4.1s;}

@keyframes fadeIn{to{opacity:1;}}
@keyframes slideIn{to{opacity:1;transform:translateY(0);}}

.vip-card{
margin:80px auto;
background:rgba(0,0,0,0.3);
border:2px solid #00eaff;
padding:40px;
max-width:400px;
border-radius:18px;
box-shadow:0 0 40px #00eaff;
backdrop-filter:blur(12px);
opacity:0;
animation:fadeIn 2s forwards;
animation-delay:4.5s;
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
<h2>VIP ZONE</h2>
<p>Daily Forex Signals</p>
<p>High Win Rate</p>
<p>Elite Access</p>
</div>
</div>

<!-- THREE JS -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r152/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.152/examples/js/loaders/GLTFLoader.js"></script>

<script>
let scene, camera, renderer, shark;
let startTime = null;
let introDone = false;

scene = new THREE.Scene();
scene.fog = new THREE.Fog(0x000000, 10, 80);

camera = new THREE.PerspectiveCamera(60, window.innerWidth/window.innerHeight, 0.1, 1000);
camera.position.set(0,0,35);

renderer = new THREE.WebGLRenderer({
canvas: document.getElementById("bgCanvas"),
antialias:true
});
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.setPixelRatio(window.devicePixelRatio);

// LIGHTING (REALISTIC)
const ambient = new THREE.AmbientLight(0x111111);
scene.add(ambient);

const keyLight = new THREE.DirectionalLight(0x00eaff, 2);
keyLight.position.set(5,10,10);
scene.add(keyLight);

const rimLight = new THREE.PointLight(0x00eaff, 3, 100);
rimLight.position.set(0,5,15);
scene.add(rimLight);

// LOAD SHARK MODEL (vendos modelin real)
const loader = new THREE.GLTFLoader();
loader.load("shark.glb", function(gltf){
shark = gltf.scene;
shark.scale.set(5,5,5);
shark.position.set(0,0,-60);
scene.add(shark);
});

// ANIMATION
function animate(timestamp){
requestAnimationFrame(animate);

if(!startTime) startTime = timestamp;
let elapsed = timestamp - startTime;

if(shark && !introDone){

// dalja nga errësira
if(elapsed < 1500){
shark.position.z += 0.08;
}

// afrimi gradual
else if(elapsed < 2500){
shark.position.z += 0.2;
camera.position.z -= 0.02;
}

// sulmi final
else if(elapsed < 3300){
shark.position.z += 0.6;
camera.position.z -= 0.1;
}

// fund intro
else{
introDone = true;
}

shark.rotation.y += 0.01;
}

// levizje e lehtë kamere
camera.position.x = Math.sin(timestamp*0.0005) * 1.5;

renderer.render(scene,camera);
}

animate();

window.addEventListener("resize", ()=>{
camera.aspect = window.innerWidth/window.innerHeight;
camera.updateProjectionMatrix();
renderer.setSize(window.innerWidth, window.innerHeight);
});
</script>

</body>
</html>
