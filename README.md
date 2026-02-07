<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For My Wife ❤️</title>

<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600&family=Playfair+Display:wght@400;600&family=Poppins:wght@300;400&display=swap" rel="stylesheet">

<style>
body{
    margin:0;
    height:100vh;
    overflow:hidden;
    font-family:'Poppins',sans-serif;
    color:#fff;
}

/* 💖 Romantic cartoon couple background */
body::before{
    content:"";
    position:fixed;
    inset:0;
    background:
      linear-gradient(rgba(255,160,190,.55),rgba(255,200,220,.55)),
      url("https://i.imgur.com/VKZQK6N.png");
    background-size:cover;
    background-position:center;
    filter:blur(9px);
    z-index:-3;
}

.overlay{
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.25);
    z-index:-2;
}

/* ❄️ Falling dots */
.dots{position:fixed;inset:0;pointer-events:none;z-index:-1;}
.dot{
    position:absolute;
    width:6px;height:6px;
    background:white;border-radius:50%;
    opacity:.6;filter:blur(1px);
    animation:fall linear infinite;
}
@keyframes fall{
    from{transform:translateY(-10vh);}
    to{transform:translateY(110vh);}
}

.center{
    position:absolute;
    top:50%;left:50%;
    transform:translate(-50%,-50%);
    width:92%;
    text-align:center;
}

/* Background Name */
.bg-name{
    position:fixed;
    top:50%;left:50%;
    transform:translate(-50%,-50%);
    font-family:'Cormorant Garamond',serif;
    font-size:46px;
    color:rgba(255,255,255,0.12);
    z-index:-1;
    pointer-events:none;
}

/* Button */
button{
    padding:10px 26px;
    font-size:14px;
    border:none;
    border-radius:24px;
    background:#ff6b9c;
    color:white;
    box-shadow:0 0 14px rgba(255,107,156,.6);
    cursor:pointer;
}

/* Text */
.first-text{font-size:15px;line-height:1.7;margin-bottom:16px;}
.hint-text{
    font-size:13px;
    opacity:.85;
    margin-bottom:14px;
    font-style:italic;
}

/* 🌹 GAME */
.grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:14px;
    justify-items:center;
}
.rose-box{
    width:75px;height:75px;
    background:rgba(255,255,255,0.12);
    border-radius:16px;
    display:flex;align-items:center;justify-content:center;
    font-size:26px;cursor:pointer;
}
.rose-box.glow{box-shadow:0 0 14px 4px rgba(255,92,138,.9);}
.counter{margin-top:15px;font-size:13px;opacity:.9;}

/* Popup */
.popup{
    position:fixed;inset:0;
    background:rgba(0,0,0,0.6);
    display:flex;align-items:center;justify-content:center;
    z-index:10;
}
.popup-card{
    background:rgba(255,255,255,0.18);
    padding:22px;border-radius:18px;
    max-width:320px;
    text-align:center;
    backdrop-filter:blur(6px);
    font-family:'Playfair Display',serif;
    font-size:14px;line-height:1.8;
}

/* 💖 STORY */
.story{
    margin-top:-40px;
    font-family:'Playfair Display',serif;
    font-size:15px;
    line-height:2;
    animation:glow 3s ease-in-out infinite;
}
@keyframes glow{
    0%{text-shadow:0 0 4px #ffb3c6;}
    50%{text-shadow:0 0 12px #ff8fab;}
    100%{text-shadow:0 0 4px #ffb3c6;}
}
</style>
</head>

<body>
<div class="overlay"></div>
<div class="dots" id="dots"></div>

<div id="bgName" class="bg-name" style="display:none;">KEERTHANA BABE</div>
<div id="app" class="center"></div>

<script>
/* dots */
const dots=document.getElementById("dots");
for(let i=0;i<30;i++){
 const d=document.createElement("div");
 d.className="dot";
 d.style.left=Math.random()*100+"%";
 d.style.animationDuration=6+Math.random()*6+"s";
 d.style.opacity=Math.random();
 dots.appendChild(d);
}

const app=document.getElementById("app");

/* PAGE 1 */
function pageOne(){
 app.innerHTML=`
 <div class="first-text">
 I made something with my heart ❤️<br>
 Only for you…<br><br>
 Tap gently 🌸
 </div>
 <button onclick="pageTwo()">Open 💗</button>`;
}

/* QUOTES */
const allQuotes=[
"You are my peace.","My heart chose you.","My wife, my home.",
"You are my forever.","My soul rests in you.","Every heartbeat is yours.",
"I fall for you every day.","You are my calm.","My love has no end.",
"You are my happiness.","My world feels safe with you.",
"I choose you always.","You are my blessing.",
"My heart belongs to you.","Forever feels right with you.",
"You are my everything.","You are my miracle.","My love lives in you."
];

let quotePool=[...allQuotes];
let taps=0;
let locked=false;

/* PAGE 2 */
function pageTwo(){
 app.innerHTML=`
 <div class="first-text">For the woman my heart chose 💖</div>

 <div class="hint-text">
 If you tap these roses 50 times… a hidden message is waiting just for you 🌹💖
 </div>

 <div class="grid" id="grid"></div>

 <div class="counter" id="counter">Love level: 0 💕</div>

 <button style="margin-top:16px" onclick="loadingPage()">
 Skip Game ❤️
 </button>
 `;
 const grid=document.getElementById("grid");
 const counter=document.getElementById("counter");

 for(let i=0;i<9;i++){
  const b=document.createElement("div");
  b.className="rose-box";
  b.innerText="🌹";
  b.onclick=()=>{
    if(locked) return;
    taps++;
    counter.innerText=`Love level: ${taps} 💕`;
    b.classList.add("glow");
    setTimeout(()=>b.classList.remove("glow"),300);
    popup(nextQuote());

    if(taps===50){
        locked=true;
        setTimeout(secretMessage,400);
    }
  };
  grid.appendChild(b);
 }
}

function nextQuote(){
 if(quotePool.length===0) quotePool=[...allQuotes];
 return quotePool.splice(Math.floor(Math.random()*quotePool.length),1)[0];
}

function popup(text){
 const p=document.createElement("div");
 p.className="popup";
 p.innerHTML=`<div class="popup-card">${text}</div>`;
 document.body.appendChild(p);
 setTimeout(()=>p.remove(),2000);
}

/* 💝 SECRET @ 50 */
function secretMessage(){
 const p=document.createElement("div");
 p.className="popup";
 p.innerHTML=`
 <div class="popup-card">
 <b>50 touches… 💖</b><br><br>
 That means you touched my heart 50 times.<br><br>
 No matter how many times you touch this world,<br>
 my heart will always respond to you first.<br><br>
 <b>I love you soooo mucchhhhhh babaaa…!! 💋😘🫂🫶🏻</b><br><br>
 <button onclick="this.closest('.popup').remove(); loadingPage();">
 Go Next ❤️
 </button>
 </div>`;
 document.body.appendChild(p);
}

/* LOADING */
function loadingPage(){
 let t=10;
 app.innerHTML=`<div class="first-text">Holding this moment…<br><span id="timer"></span></div>`;
 const i=setInterval(()=>{
 document.getElementById("timer").innerText=t+" seconds";
 t--;
 if(t<0){clearInterval(i);finalPage();}
 },1000);
}

/* FINAL PAGE */
function finalPage(){
 document.getElementById("bgName").style.display="block";
 app.innerHTML=`
 <img src="95F906A3-2874-41DE-849E-CEE9D331A599.png" width="220"><br><br>

 <div class="story">
 Somewhere between ordinary days and quiet nights,<br>
 my heart chose you without asking why.<br><br>

 You are my calm, my strength,<br>
 my happiness in moments I never want to end.<br><br>

 Loving you is not something I promise,<br>
 it is something I live every single day.<br><br>

 <b>I love you babee ❤️</b><br><br>

 Happy Rose Day, my wife 🌹<br>
 <b>Keerthana Babe</b>, you are my forever ❤️
 </div><br>

 <button onclick="window.location.href='https://snapchat.com/t/L2LELgMn'">
 Send Me More Love 💖
 </button>`;
}

pageOne();
</script>
</body>
</html>
