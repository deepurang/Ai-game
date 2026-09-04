# Ai-game<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Quiz Battle V5</title>

<style>
*{box-sizing:border-box}

body{
 margin:0;
 font-family:Arial,sans-serif;
 background:linear-gradient(135deg,#090b22,#17134b,#081b35);
 color:#fff;
 min-height:100vh
}

.app{
 max-width:520px;
 margin:auto;
 padding:16px
}

.top{
 display:flex;
 justify-content:space-between;
 align-items:center;
 margin-bottom:14px
}

.card{
 background:rgba(255,255,255,.09);
 border:1px solid rgba(255,255,255,.13);
 border-radius:20px;
 padding:18px;
 margin:12px 0;
 box-shadow:0 10px 30px rgba(0,0,0,.25)
}

h1,h2,h3{margin:6px 0 12px}

.logo{
 font-size:25px;
 font-weight:800
}

.muted{
 color:#b9bed8;
 font-size:14px
}

.coins{
 background:rgba(255,214,70,.13);
 padding:9px 12px;
 border-radius:14px;
 color:#ffe36b;
 font-weight:700
}

button,select,input{
 width:100%;
 padding:13px;
 border:0;
 border-radius:13px;
 font-size:16px;
 margin:6px 0
}

button{
 background:#fff;
 color:#111;
 font-weight:700;
 cursor:pointer
}

button.primary{
 background:linear-gradient(90deg,#7c5cff,#19c7ff);
 color:#fff
}

button.secondary{
 background:rgba(255,255,255,.12);
 color:#fff
}

.grid{
 display:grid;
 grid-template-columns:1fr 1fr;
 gap:10px
}

.topic{
 padding:16px;
 text-align:left
}

.topic b{
 display:block;
 margin-bottom:4px
}

.row{
 display:flex;
 gap:8px
}

.row>*{flex:1}

.bar{
 height:8px;
 background:#ffffff18;
 border-radius:9px;
 overflow:hidden
}

.fill{
 height:100%;
 background:#19c7ff;
 width:0;
 transition:.3s
}

.q{
 font-size:21px;
 line-height:1.35;
 margin:18px 0
}

.ans{
 text-align:left;
 background:rgba(255,255,255,.1);
 color:#fff
}

.ans.correct{
 background:#1d9b67
}

.ans.wrong{
 background:#b94158
}

.stats{
 display:flex;
 justify-content:space-between;
 font-size:14px;
 color:#cdd2eb
}

.hidden{display:none}

.badge{
 display:inline-block;
 padding:7px 10px;
 background:#ffffff12;
 border-radius:12px;
 margin:4px;
 font-size:13px
}

.notice{
 padding:10px;
 border-radius:12px;
 background:#102d45;
 color:#aee7ff;
 font-size:13px;
 margin-top:10px
}

.small{
 font-size:12px;
 color:#9da4c4
}

.center{text-align:center}

.correct-answer{
 margin-top:10px;
 padding:10px;
 background:#1d9b6740;
 border-radius:10px;
 color:#9ff0c9
}
</style>
</head>

<body>

<div class="app">

<div class="top">
 <div class="logo">
 🤖 AI Quiz Battle <span style="font-size:12px">V5</span>
 </div>

 <div class="coins">
 🪙 <span id="coins">0</span>
 </div>
</div>


<!-- HOME -->

<section id="home" class="screen">

<div class="card">

<h2>Welcome, <span id="homeName">Player</span> 👋</h2>

<p class="muted">
Choose a topic and battle through smart quiz questions.
</p>

<div class="row">

<button class="primary" onclick="show('topics')">
🎮 Start Battle
</button>

<button class="secondary" onclick="daily()">
🎁 Daily
</button>

</div>

<div class="notice">
V5 Demo Mode: Your progress is saved on this device.
</div>

</div>


<div class="card">

<h3>📊 Your Stats</h3>

<div class="stats">
<span>Best Score</span>
<b id="best">0</b>
</div>

<div class="stats">
<span>Games Played</span>
<b id="games">0</b>
</div>

<div class="stats">
<span>Win Streak</span>
<b id="streak">0</b>
</div>

</div>


<div class="card">

<h3>🏅 Achievements</h3>

<div id="badges"></div>

</div>


<button class="secondary" onclick="profile()">
👤 Profile
</button>

<button class="secondary" onclick="leaderboard()">
🏆 Leaderboard
</button>

</section>


<!-- TOPICS -->

<section id="topics" class="screen hidden">

<div class="card">

<h2>🎯 Select Topic</h2>

<p class="muted">
Each battle has exactly 10 questions.
</p>

<div class="grid">

<button class="topic" onclick="start('GK')">
🌍
<b>General Knowledge</b>
<span class="small">10 questions</span>
</button>

<button class="topic" onclick="start('Science')">
🔬
<b>Science</b>
<span class="small">10 questions</span>
</button>

<button class="topic" onclick="start('Technology')">
💻
<b>Technology</b>
<span class="small">10 questions</span>
</button>

<button class="topic" onclick="start('Sports')">
⚽
<b>Sports</b>
<span class="small">10 questions</span>
</button>

<button class="topic" onclick="start('History')">
🏛️
<b>History</b>
<span class="small">10 questions</span>
</button>

<button class="topic" onclick="start('Mixed')">
🎲
<b>Mixed</b>
<span class="small">10 questions</span>
</button>

</div>

<button class="secondary" onclick="show('home')">
← Back
</button>

</div>

</section>


<!-- GAME -->

<section id="game" class="screen hidden">

<div class="card">

<div class="stats">

<span id="progress">
Question 1/10
</span>

<span>
❤️ <b id="lives">3</b>
&nbsp;
⏱️ <b id="timer">15</b>
</span>

</div>


<div class="bar">

<div id="fill" class="fill"></div>

</div>


<div id="question" class="q"></div>

<div id="answers"></div>


<button class="secondary" onclick="hint()">
🤖 AI Hint — 10 coins
</button>

<p id="hintText" class="muted"></p>

</div>

</section>


<!-- RESULT -->

<section id="result" class="screen hidden">

<div class="card center">

<h1>🏆 Battle Complete!</h1>

<h2 id="resultScore">
Score: 0
</h2>

<p id="resultMsg"></p>

<p>
🪙 Coins earned:
<b id="earned">0</b>
</p>

<button class="primary" onclick="show('topics')">
⚔️ Play Again
</button>

<button class="secondary" onclick="show('home')">
🏠 Home
</button>

</div>

</section>


<!-- EXTRA -->

<section id="extra" class="screen hidden"></section>

</div>


<script>

/* =========================
   STORAGE
========================= */

const KEY={
 name:'v5_name',
 coins:'v5_coins',
 best:'v5_best',
 games:'v5_games',
 streak:'v5_streak',
 daily:'v5_daily',
 badges:'v5_badges'
};


/* =========================
   PLAYER DATA
========================= */

let name=localStorage.getItem(KEY.name)||'Player';

let coins=Number(localStorage.getItem(KEY.coins)||0);

let best=Number(localStorage.getItem(KEY.best)||0);

let games=Number(localStorage.getItem(KEY.games)||0);

let streak=Number(localStorage.getItem(KEY.streak)||0);


/* =========================
   GAME VARIABLES
========================= */

let topic='';

let questions=[];

let idx=0;

let score=0;

let lives=3;

let timer=15;

let tick=null;

let locked=false;

let earnedThis=0;


/* =========================
   QUESTION BANK
========================= */

const banks={

GK:[

['What is the capital of India?',['New Delhi','Mumbai','Kolkata','Chennai'],0],

['Which is the largest ocean?',['Atlantic','Indian','Pacific','Arctic'],2],

['How many days are in a leap year?',['364','365','366','367'],2],

['Which planet is called the Red Planet?',['Venus','Mars','Jupiter','Mercury'],1],

['What is the national animal of India?',['Lion','Tiger','Elephant','Peacock'],1],

['Which continent is India in?',['Europe','Asia','Africa','Australia'],1],

['What is the currency of India?',['Dollar','Euro','Rupee','Pound'],2],

['How many states are there in India?',['26','28','30','32'],1],

['Which is the highest mountain in the world?',['K2','Mount Everest','Kangchenjunga','Makalu'],1],

['Which is the largest planet in our solar system?',['Earth','Mars','Jupiter','Saturn'],2]

],


Science:[

['What gas do humans need for breathing?',['Oxygen','Helium','Carbon dioxide','Hydrogen'],0],

['Water freezes at what temperature on Celsius scale?',['0°C','10°C','50°C','100°C'],0],

['Which organ pumps blood?',['Lung','Brain','Heart','Kidney'],2],

['What is H2O commonly known as?',['Salt','Water','Oxygen','Hydrogen'],1],

['Which force pulls objects toward Earth?',['Magnetism','Gravity','Friction','Electricity'],1],

['Plants mainly use which gas for photosynthesis?',['Oxygen','Nitrogen','Carbon dioxide','Helium'],2],

['How many bones are there in an adult human body?',['106','206','306','406'],1],

['What is the nearest star to Earth?',['Moon','Mars','Sun','Venus'],2],

['Which part of a plant absorbs water?',['Flower','Root','Fruit','Leaf'],1],

['What is the boiling point of water at sea level?',['50°C','75°C','100°C','150°C'],2]

],


Technology:[

['What does CPU stand for?',['Central Processing Unit','Computer Power Utility','Core Program User','Central Phone Unit'],0],

['Which device is commonly used to scan a QR code?',['Phone camera','Speaker','Keyboard','Printer'],0],

['What does Wi-Fi mainly provide?',['Wireless network connection','Electricity','Water','GPS satellites'],0],

['Which is an operating system?',['Android','Chrome','Google','YouTube'],0],

['What is a web browser used for?',['Accessing websites','Charging phones','Printing money','Measuring temperature'],0],

['What does AI commonly mean?',['Artificial Intelligence','Automatic Internet','Advanced Input','App Interface'],0],

['Which company developed Android?',['Google','Nike','Toyota','NASA'],0],

['What does URL stand for?',['Uniform Resource Locator','Universal Radio Link','User Read Line','United Resource List'],0],

['Which device is mainly used to type text?',['Keyboard','Monitor','Speaker','Mouse pad'],0],

['What does RAM help a computer with?',['Temporary working memory','Printing','Internet cables','Battery charging'],0]

],


Sports:[

['How many players are on a football/soccer team on the field?',['9','10','11','12'],2],

['Which sport uses a racket and shuttlecock?',['Tennis','Badminton','Hockey','Cricket'],1],

['How many rings are on the Olympic symbol?',['4','5','6','7'],1],

['Which sport is associated with Wimbledon?',['Cricket','Tennis','Football','Boxing'],1],

['How many wickets are there in a cricket innings team?',['8','9','10','11'],2],

['Which sport uses a bat and ball and has bases?',['Baseball','Swimming','Golf','Boxing'],0],

['How many players are there in a cricket team?',['9','10','11','12'],2],

['Which country hosted the 2016 Summer Olympics?',['China','Brazil','India','Japan'],1],

['In which sport is the term "checkmate" used?',['Chess','Football','Cricket','Tennis'],0],

['Which sport is played at the Tour de France?',['Cycling','Boxing','Golf','Tennis'],0]

],


History:[

['Who was known as the Father of the Indian Constitution?',['B. R. Ambedkar','Mahatma Gandhi','Sardar Patel','Jawaharlal Nehru'],0],

['India became independent in which year?',['1942','1945','1947','1950'],2],

['Who built the Taj Mahal?',['Akbar','Shah Jahan','Aurangzeb','Babur'],1],

['The Quit India Movement began in which year?',['1930','1942','1947','1952'],1],

['Who was the first Prime Minister of independent India?',['Rajendra Prasad','Jawaharlal Nehru','Sardar Patel','B. R. Ambedkar'],1],

['Republic Day in India is celebrated on?',['15 August','26 January','2 October','14 November'],1],

['Who is known as the Father of the Nation in India?',['Mahatma Gandhi','Subhas Chandra Bose','Bhagat Singh','Jawaharlal Nehru'],0],

['Who was the first President of India?',['Rajendra Prasad','Sardar Patel','Nehru','Ambedkar'],0],

['The Indian Constitution came into effect in which year?',['1947','1948','1950','1952'],2],

['Who founded the Maurya Empire?',['Ashoka','Chandragupta Maurya','Akbar','Harsha'],1]

]

};


/* =========================
   SAVE
========================= */

function save(){

 localStorage.setItem(KEY.name,name);

 localStorage.setItem(KEY.coins,coins);

 localStorage.setItem(KEY.best,best);

 localStorage.setItem(KEY.games,games);

 localStorage.setItem(KEY.streak,streak);

 update();

}


/* =========================
   UPDATE UI
========================= */

function update(){

 document.getElementById('coins').textContent=coins;

 document.getElementById('homeName').textContent=name;

 document.getElementById('best').textContent=best;

 document.getElementById('games').textContent=games;

 document.getElementById('streak').textContent=streak;


 let b=[];

 if(games>=1)
 b.push('🎮 First Battle');

 if(best>=50)
 b.push('⭐ 50+ Score');

 if(streak>=3)
 b.push('🔥 3 Win Streak');

 if(coins>=100)
 b.push('🪙 100 Coins');


 if(b.length===0){

 b.push('<span class="small">Play to unlock badges!</span>');

 }


 document.getElementById('badges').innerHTML=
 b.map(x=>'<span class="badge">'+x+'</span>').join('');

}


/* =========================
   SCREEN
========================= */

function show(id){

 document.querySelectorAll('.screen')
 .forEach(x=>x.classList.add('hidden'));

 document.getElementById(id)
 .classList.remove('hidden');

 update();

}


/* =========================
   SHUFFLE
========================= */

function shuffle(array){

 return array
 .slice()
 .sort(()=>Math.random()-0.5);

}


/* =========================
   START GAME
========================= */

function start(t){

 topic=t;

 let pool;

 if(t==='Mixed'){

 pool=Object.values(banks).flat();

 }else{

 pool=banks[t];

 }


 questions=shuffle(pool).slice(0,10);

 idx=0;

 score=0;

 lives=3;

 earnedThis=0;

 show('game');

 loadQ();

}


/* =========================
   LOAD QUESTION
========================= */

function loadQ(){

 if(idx>=questions.length){

 finish();

 return;

 }


 locked=false;

 timer=15;

 document.getElementById('hintText').textContent='';


 const q=questions[idx];


 const order=shuffle(

 q[1].map((text,i)=>({

 text:text,

 i:i

 }))

 );


 document.getElementById('progress').textContent=
 `Question ${idx+1}/10`;


 document.getElementById('lives').textContent=lives;

 document.getElementById('timer').textContent=timer;


 document.getElementById('fill').style.width=
 ((idx)/10*100)+'%';


 document.getElementById('question').textContent=q[0];


 document.getElementById('answers').innerHTML=

 order.map(o=>

 `<button class="ans"
 onclick="answer(this,${o.i},${q[2]})">
 ${o.text}
 </button>`

 ).join('');


 clearInterval(tick);


 tick=setInterval(()=>{

 timer--;

 document.getElementById('timer').textContent=timer;


 if(timer<=0){

 clearInterval(tick);

 answer(null,-1,q[2]);

 }

 },1000);

}


/* =========================
   ANSWER
========================= */

function answer(btn,chosen,correct){

 if(locked)return;

 locked=true;

 clearInterval(tick);


 if(chosen===correct){

 score+=10;

 coins+=10;

 earnedThis+=10;


 if(btn)
 btn.classList.add('correct');


 }else{

 lives--;


 if(btn)
 btn.classList.add('wrong');


 document
 .querySelectorAll('.ans')
 .forEach(b=>{

 if(
 b.textContent.trim()===
 questions[idx][1][correct]
 ){

 b.classList.add('correct');

 }

 });


 }


 document.getElementById('lives').textContent=lives;


 save();


 setTimeout(()=>{

 if(lives<=0){

 finish();

 }else{

 idx++;

 loadQ();

 }

 },700);

}


/* =========================
   HINT
========================= */

function hint(){

 if(locked)return;


 if(coins<10){

 document.getElementById('hintText').textContent=
 '❌ Not enough coins.';

 return;

 }


 coins-=10;

 save();


 let q=questions[idx];


 let wrong=q[1]
 .filter((_,i)=>i!==q[2])
 .slice(0,2)
 .join(' / ');


 document.getElementById('hintText').textContent=
 '🤖 Hint: Two possible wrong options are '+wrong;

}


/* =========================
   FINISH
========================= */

function finish(){

 clearInterval(tick);


 games++;


 let bonus=20+(lives*10);


 if(topic==='Mixed')
 bonus+=10;


 coins+=bonus;

 earnedThis+=bonus;


 if(score>best)
 best=score;


 if(score>=50)
 streak++;
 else
 streak=0;


 save();


 document.getElementById('resultScore').textContent=
 'Score: '+score;


 document.getElementById('earned').textContent=
 earnedThis;


 document.getElementById('resultMsg').textContent=

 score>=70
 ?'🔥 Excellent battle!'
 :score>=40
 ?'👏 Good job!'
 :'💪 Keep practicing!';


 show('result');

}


/* =========================
   DAILY REWARD
========================= */

function daily(){

 let today=new Date().toDateString();


 if(localStorage.getItem(KEY.daily)===today){

 alert(
 'Daily reward already claimed today. Come back tomorrow!'
 );

 return;

 }


 coins+=50;


 localStorage.setItem(KEY.daily,today);


 save();


 alert('🎁 Daily reward: +50 coins!');

}


/* =========================
   PROFILE
========================= */

function profile(){

 let safeName=name
 .replace(/"/g,'&quot;')
 .replace(/</g,'&lt;')
 .replace(/>/g,'&gt;');


 document.getElementById('extra').innerHTML=

 `<div class="card">

 <h2>👤 Profile</h2>

 <input
 id="nameInput"
 value="${safeName}"
 maxlength="20"
 placeholder="Enter your name">

 <button class="primary"
 onclick="saveProfile()">
 Save Name
 </button>

 <button class="secondary"
 onclick="show('home')">
 ← Back
 </button>

 </div>`;


 show('extra');

}


/* =========================
   SAVE PROFILE
========================= */

function saveProfile(){

 let v=
 document.getElementById('nameInput')
 .value
 .trim();


 if(v){

 name=v;

 save();

 show('home');

 }

}


/* =========================
   LEADERBOARD
========================= */

function leaderboard(){

 let scores=
 JSON.parse(
 localStorage.getItem('v5_lb')||'[]'
 );


 scores.push({

 name:name,

 score:best

 });


 scores=
 scores
 .sort((a,b)=>b.score-a.score)
 .slice(0,10);


 localStorage.setItem(
 'v5_lb',
 JSON.stringify(scores)
 );


 document.getElementById('extra').innerHTML=

 `<div class="card">

 <h2>🏆 Leaderboard</h2>

 ${scores.map((s,i)=>

 `<div class="stats"
 style="padding:9px 0">

 <span>
 ${i+1}. ${s.name}
 </span>

 <b>${s.score}</b>

 </div>`

 ).join('')}

 <p class="small">
 Demo leaderboard: stored on this device only.
 </p>

 <button
 class="secondary"
 onclick="show('home')">
 ← Back
 </button>

 </div>`;


 show('extra');

}


/* =========================
   INITIALIZE
========================= */

update();

</script>

</body>
</html>
