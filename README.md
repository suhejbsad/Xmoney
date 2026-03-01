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
const gl = canvas.getContext("webgl");

function resize(){
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  gl.viewport(0,0,gl.drawingBufferWidth,gl.drawingBufferHeight);
}
resize();
window.addEventListener("resize", resize);

const vertexShaderSource = `
attribute vec2 position;
void main(){
  gl_Position = vec4(position,0.0,1.0);
}
`;

const fragmentShaderSource = `
precision highp float;
uniform vec2 u_resolution;
uniform float u_time;

float random(vec2 st){
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}

void main(){
    vec2 uv = gl_FragCoord.xy / u_resolution.xy;
    uv -= 0.5;
    uv.x *= u_resolution.x / u_resolution.y;

    float t = u_time * 2.0;

    float wave = sin(uv.x*20.0 + t) * cos(uv.y*15.0 - t);
    float energy = abs(wave);

    float glow = 0.02 / (abs(wave) + 0.02);

    vec3 base = vec3(0.0, 0.0, 0.05);
    vec3 electric = vec3(0.0,0.8,1.0) * glow * 2.0;

    vec3 color = base + electric * energy;

    gl_FragColor = vec4(color,1.0);
}
`;

function createShader(type, source){
  const shader = gl.createShader(type);
  gl.shaderSource(shader, source);
  gl.compileShader(shader);
  return shader;
}

const vertexShader = createShader(gl.VERTEX_SHADER, vertexShaderSource);
const fragmentShader = createShader(gl.FRAGMENT_SHADER, fragmentShaderSource);

const program = gl.createProgram();
gl.attachShader(program, vertexShader);
gl.attachShader(program, fragmentShader);
gl.linkProgram(program);
gl.useProgram(program);

const positionBuffer = gl.createBuffer();
gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([
  -1,-1,
   1,-1,
  -1, 1,
  -1, 1,
   1,-1,
   1, 1
]), gl.STATIC_DRAW);

const positionLocation = gl.getAttribLocation(program,"position");
gl.enableVertexAttribArray(positionLocation);
gl.vertexAttribPointer(positionLocation,2,gl.FLOAT,false,0,0);

const resolutionLocation = gl.getUniformLocation(program,"u_resolution");
const timeLocation = gl.getUniformLocation(program,"u_time");

function render(time){
  gl.uniform2f(resolutionLocation,canvas.width,canvas.height);
  gl.uniform1f(timeLocation,time*0.001);
  gl.drawArrays(gl.TRIANGLES,0,6);
  requestAnimationFrame(render);
}
requestAnimationFrame(render);

function joinVIP(){ alert("Welcome to the VIP zone!"); }
</script>

</body>
</html>
