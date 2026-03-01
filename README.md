<script>
const canvas = document.getElementById("chart");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let candles = [];
let offset = 0;

function generateCandles(){
    candles = [];
    let base = canvas.height / 2;

    for(let i=0; i<120; i++){
        let open = base + (Math.random() - 0.5) * 200;
        let close = open + (Math.random() - 0.5) * 150;
        let high = Math.max(open, close) + Math.random() * 80;
        let low = Math.min(open, close) - Math.random() * 80;

        candles.push({ x: i * 15, open, close, high, low });
    }
}

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
        ctx.lineTo(canvas.width, j);
        ctx.stroke();
    }
}

function drawCandles(){
    candles.forEach(c=>{
        let x = c.x - offset;

        // Wick
        ctx.strokeStyle = "rgba(255,215,0,0.6)";
        ctx.beginPath();
        ctx.moveTo(x + 4, c.high);
        ctx.lineTo(x + 4, c.low);
        ctx.stroke();

        // Body
        if(c.close > c.open){
            ctx.fillStyle = "gold";
            ctx.fillRect(x, c.open, 8, c.close - c.open);
        } else {
            ctx.fillStyle = "white";
            ctx.fillRect(x, c.close, 8, c.open - c.close);
        }
    });
}

function animate(){
    ctx.clearRect(0,0,canvas.width,canvas.height);

    drawGrid();
    drawCandles();

    offset += 1;

    if(offset > candles.length * 15){
        generateCandles();
        offset = 0;
    }

    requestAnimationFrame(animate);
}

generateCandles();
animate();

window.addEventListener("resize", ()=>{
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    generateCandles();
});
</script>
