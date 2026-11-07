# SUBHAM-RUNNER-PRO
SUBHAM MOD RUNNER

<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Subham Runner Pro</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;background:#101820;color:white;
 font-family:Arial;text-align:center;
}
h1{color:#ffd43b;margin:12px}
#info{font-size:20px;margin:10px}
#game{
 position:relative;
 width:95%;max-width:420px;
 height:540px;margin:auto;
 overflow:hidden;
 background:linear-gradient(#8bd5ff,#4c8c42);
 border:4px solid white;border-radius:12px;
}
#road{
 position:absolute;left:15%;width:70%;
 height:100%;background:#444;
 border-left:5px solid white;
 border-right:5px solid white;
}
.line{
 position:absolute;top:0;bottom:0;
 left:33.33%;border-left:3px dashed white;
}
.line.two{left:66.66%}
#player{
 position:absolute;bottom:15px;
 left:50%;transform:translateX(-50%);
 font-size:45px;z-index:5;
}
.object{
 position:absolute;font-size:35px;
 transform:translateX(-50%);
 z-index:4;
}
#controls{margin:12px}
button{
 background:#ffbd00;border:0;
 padding:15px 28px;margin:5px;
 border-radius:12px;font-size:20px;
 font-weight:bold;
}
</style>
</head>
<body>

<h1>🏃 SUBHAM RUNNER PRO</h1>
<div id="info">
 Score: <span id="score">0</span>
 | Coins: <span id="coins">0</span>
</div>

<div id="game">
 <div id="road">
  <div class="line"></div>
  <div class="line two"></div>
 </div>
 <div id="player">🏃</div>
</div>

<div id="controls">
 <button onclick="move(-1)">⬅️</button>
 <button onclick="start()">START</button>
 <button onclick="move(1)">➡️</button>
</div>
<p id="msg">Press START to play!</p>

<script>
let lane=1,score=0,coins=0;
let playing=false,objects=[];
let speed=3,loop=null;

const game=document.getElementById("game");
const player=document.getElementById("player");

function position(){
 player.style.left=(15+lane*35)+"%";
}

function move(dir){
 if(!playing)return;
 lane=Math.max(0,Math.min(2,lane+dir));
 position();
}

function createObject(){
 let el=document.createElement("div");
 let coin=Math.random()<0.55;
 el.className="object";
 el.innerText=coin?"🪙":"🚧";
 let l=Math.floor(Math.random()*3);
 el.style.left=(32.5+l*17.5)+"%";
 el.style.top="-45px";
 game.appendChild(el);
 objects.push({el,lane:l,y:-45,coin});
}

function start(){
 clearInterval(loop);
 objects.forEach(o=>o.el.remove());
 objects=[];
 lane=1;score=0;coins=0;
 speed=3;playing=true;
 position();update();
 document.getElementById("msg").innerText="RUN!";
 loop=setInterval(tick,30);
}

function update(){
 document.getElementById("score").innerText=score;
 document.getElementById("coins").innerText=coins;
}

function tick(){
 score++;
 if(score%65===0)createObject();
 if(score%500===0)speed+=0.5;

 objects.forEach(o=>{
  o.y+=speed;
  o.el.style.top=o.y+"px";

  if(o.y>440 && o.y<510 && o.lane===lane){
   if(o.coin){
    coins++;o.y=600;
   }else{
    endGame yes();
   }
   update();
  }
 });

 objects=objects.filter(o=>{
  if(o.y>550){o.el.remove();return false}
  return true;
 });
 update();
}

function endGame(){
 playing=false;
 clearInterval(loop);
 document.getElementById("msg").innerText=
 "GAME OVER! Score: "+score;
}

document.addEventListener("keydown",e=>{
 if(e.key==="ArrowLeft")move(-1);
 if(e.key==="ArrowRight")move(1);
});
</script>
</body>
</html>
