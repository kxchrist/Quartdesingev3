# Quartdesingev3
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quart de Singe 🐒</title>

  <!-- Logo pour l’icône de l’app -->
  <link rel="icon" href="logo.png" type="image/png">

  <!-- Optionnel : style général pour fond, police, bouton -->
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Comic+Neue:wght@700&display=swap');
    body {
      font-family: 'Comic Neue', cursive;
      text-align: center;
      background: linear-gradient(to bottom, #fff176, #ffb74d); /* fond jaune-orange */
      color: #4e342e;
      margin: 0;
    }
    button {
      font-size: 20px;
      padding: 12px 25px;
      margin-top: 20px;
      cursor: pointer;
      background-color: #ffeb3b;
      border: 2px solid #fbc02d;
      border-radius: 12px;
    }
    button:hover {
      background-color: #fdd835;
    }
  </style>
</head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quart de Singe</title>

<style>

body{
font-family:Arial;
background:linear-gradient(135deg,#1e1e1e,#3c3c3c);
color:white;
text-align:center;
margin:0;
padding:20px;
}

h1{
margin-bottom:5px;
}

.rules{
background:#2a2a2a;
padding:10px;
border-radius:10px;
margin-bottom:15px;
font-size:14px;
}

.controls{
margin-bottom:15px;
}

input{
padding:10px;
border-radius:8px;
border:none;
}

button{
padding:10px 14px;
border:none;
border-radius:8px;
background:#ff9800;
color:white;
font-weight:bold;
margin:4px;
}

button:hover{
opacity:0.8;
}

#players{
display:flex;
flex-direction:column;
gap:12px;
margin-top:15px;
}

.player{
background:#2c2c2c;
padding:15px;
border-radius:12px;
box-shadow:0 5px 10px rgba(0,0,0,0.4);
transition:0.3s;
}

.player.singe{
background:#4b2b2b;
border:2px solid #ff5252;
animation:singeFlash 0.5s 3;
}

@keyframes singeFlash{
0%{transform:scale(1)}
50%{transform:scale(1.05)}
100%{transform:scale(1)}
}

.progress{
height:10px;
background:#555;
border-radius:10px;
overflow:hidden;
margin:8px 0;
}

.bar{
height:100%;
background:#ff9800;
width:0%;
}

.shots{
font-size:18px;
margin-top:10px;
}

.ruleBox{
margin-top:10px;
background:#444;
padding:10px;
border-radius:10px;
}

</style>
</head>

<body>

<h1>🐒 Quart de Singe</h1>

<div class="rules">
Rappel :<br>
• Si quelqu’un rit → +1 quart + shot 🍻<br>
• Si quelqu’un regarde un singe → +1 quart + shot<br>
• À 4 quarts → 🐒 SINGE<br>
• Les singes peuvent provoquer les autres
</div>

<div class="controls">

<input id="name" placeholder="Nom du joueur">
<button onclick="addPlayer()">Ajouter</button>

<br>

<button onclick="randomRule()">🎲 Règle aléatoire</button>
<button onclick="resetGame()">🔄 Reset</button>

</div>

<div class="ruleBox" id="ruleBox">
Aucune règle spéciale pour l'instant
</div>

<div class="shots">
🍻 Shots bus : <span id="shotCount">0</span>
</div>

<div id="players"></div>

<script>

let players=[]
let shots=0

let rules=[
"Interdiction de dire 'oui'",
"Interdiction de croiser les bras",
"Parler avec un accent",
"Interdiction de dire un prénom",
"Interdiction de pointer quelqu'un du doigt",
"Tout le monde doit parler lentement",
"Interdiction de dire 'je'",
"Dire 'banane' avant chaque phrase",
"Interdiction de poser une question",
"Parler comme un robot"
]

function addPlayer(){

let name=document.getElementById("name").value
if(name==="")return

players.push({name:name,quart:0})

document.getElementById("name").value=""

render()

}

function addQuart(i){

if(players[i].quart>=4)return

players[i].quart++

shots++
document.getElementById("shotCount").innerText=shots

render()

}

function randomRule(){

let rule=rules[Math.floor(Math.random()*rules.length)]

document.getElementById("ruleBox").innerText="🎲 Nouvelle règle : "+rule

}

function resetGame(){

players=[]
shots=0

document.getElementById("shotCount").innerText=0
document.getElementById("ruleBox").innerText="Aucune règle spéciale pour l'instant"

render()

}

function render(){

let html=""

players.forEach((p,i)=>{

let percent=(p.quart/4)*100
let singe=p.quart>=4

html+=`
<div class="player ${singe?'singe':''}">
<h3>${p.name}</h3>

<div>${singe?'🐒 SINGE':'Humain'}</div>

<div class="progress">
<div class="bar" style="width:${percent}%"></div>
</div>

<div>${p.quart} / 4 quarts</div>

<button onclick="addQuart(${i})">+1 Quart</button>

</div>
`

})

document.getElementById("players").innerHTML=html

}

</script>

</body>
</html>
