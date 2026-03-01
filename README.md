<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Xmoney</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600;800&family=Cinzel:wght@600&display=swap" rel="stylesheet">
<style>
body, html {margin:0; padding:0; overflow:hidden; background:#000; font-family:'Poppins', sans-serif;}
#introVideo {position:fixed; top:0; left:0; width:100%; height:100%; object-fit:cover; z-index:999;}
.container {opacity:0; transition:opacity 1s ease; position:relative; z-index:1; text-align:center; padding:100px 20px;}
.title {font-family:'Cinzel', serif; font-size:240px; color:white; letter-spacing:5px; opacity:0; animation:fadeIn 2s forwards 0.2s;}
.subtitle {margin-top:20px; font-size:20px; color:white; opacity:0; transform:translateY(20px); animation:slideIn 1.5s forwards;}
.subtitle:nth-child(2){animation-delay:0.5s;} .subtitle:nth-child(3){animation-delay:0.8s;} .subtitle:nth-child(4){animation-delay:1.1s;}
@keyframes fadeIn {0%{opacity:0;}100%{opacity:1;}}
@keyframes slideIn {to{opacity:1; transform:translateY(0);}}
.vip-card {margin:80px auto; background:rgba(0,0,0,0.3); border:2px solid #0ff; padding:40px; width:90%; max-width:400px; border-radius:18px; box-shadow:0 0 30px #0ff; backdrop-filter:blur(12px); transition:0.5s;}
.vip-card:hover {transform:translateY(-8px); box-shadow:0 0 50px #0ff;}
.vip-title {font-family:'Cinzel', serif; font-size:28px; margin-bottom:20px; color:#0ff;}
.vip-text {margin:10px 0; color:#0ff; opacity:0; transform:translateY(20px); animation:slideIn 1.5s forwards;}
.vip-text:nth-child(2){animation-delay:1.2s;} .vip-text:nth-child(3){animation-delay:1.5s;} .vip-text:nth-child(4){animation-delay:1.8s;}
.join-btn {margin-top:20px; padding:12px 30px; background:#0ff; border:none; border-radius:8px; color:black; font-size:16px; font-weight:bold; cursor:pointer; transition:0.3s;}
.join-btn:hover {background:white; color:#0ff;}
#memberCounter {margin-top:20px; font-size:20px; color:white; text-align:center; font-weight:bold;}
</style>
</head>
<body>

<!-- VIDEO INTRO 3 SEKONDA -->
<video id="introVideo" autoplay muted playsinline>
  <source src="/mnt/data/a_3d_rendered_animated_scene_lasts_for_three_secon.png" type="video/mp4">
</video>

<!-- MAIN CONTENT -->
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

<script>
// kur video perfundon, fsheh video dhe shfaq faqen
const introVideo = document.getElementById("introVideo");
const mainContent = document.getElementById("mainContent");

introVideo.onended = () => {
  introVideo.style.display = "none";
  mainContent.style.opacity = 1;
};

// MEMBER COUNTER
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
