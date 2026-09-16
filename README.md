<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">

<title>Greece Weather — 15ήμερη Πρόγνωση</title>

<style>
*{box-sizing:border-box;margin:0;padding:0}

body{
font-family:Arial,sans-serif;
background:linear-gradient(160deg,#071a32,#0d4675,#09243e);
color:white;
min-height:100vh;
}

header{
text-align:center;
padding:35px 15px 25px;
background:rgba(0,0,0,.2);
}

header h1{
font-size:34px;
margin-bottom:10px;
}

header p{
opacity:.85;
font-size:16px;
}

.container{
max-width:1200px;
margin:auto;
padding:20px 15px 40px;
}

.search{
display:flex;
gap:10px;
margin-bottom:25px;
}

.search input{
flex:1;
padding:16px;
border:0;
border-radius:14px;
font-size:16px;
outline:none;
}

.search button{
border:0;
border-radius:14px;
padding:0 22px;
font-weight:bold;
cursor:pointer;
}

.section-title{
font-size:24px;
margin:28px 0 15px;
}

.cities{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(145px,1fr));
gap:10px;
}

.city-button{
border:0;
border-radius:15px;
padding:16px 10px;
background:rgba(255,255,255,.12);
color:white;
cursor:pointer;
font-size:15px;
transition:.2s;
}

.city-button:hover{
background:rgba(255,255,255,.23);
transform:translateY(-2px);
}

.current{
margin-top:25px;
padding:25px;
border-radius:22px;
background:rgba(255,255,255,.12);
text-align:center;
}

.current h2{
font-size:27px;
}

.temp{
font-size:65px;
font-weight:bold;
margin:12px;
}

.status{
font-size:19px;
margin-bottom:20px;
}

.details{
display:grid;
grid-template-columns:repeat(4,1fr);
gap:10px;
}

.detail{
background:rgba(0,0,0,.16);
border-radius:14px;
padding:15px;
}

.forecast{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(145px,1fr));
gap:12px;
}

.day{
background:rgba(255,255,255,.12);
border-radius:17px;
padding:17px 10px;
text-align:center;
}

.day .date{
font-weight:bold;
font-size:16px;
}

.day .icon{
font-size:35px;
margin:10px;
}

.day .max{
font-size:24px;
font-weight:bold;
}

.day .min{
opacity:.7;
margin-top:5px;
}

.day .rain{
margin-top:10px;
font-size:14px;
}

.models{
margin-top:15px;
background:rgba(0,0,0,.18);
padding:17px;
border-radius:15px;
font-size:14px;
line-height:1.6;
}

.maps{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:12px;
}

.mapbutton{
border:0;
border-radius:17px;
padding:22px;
background:rgba(255,255,255,.12);
color:white;
font-size:17px;
cursor:pointer;
}

.mapbutton:hover{
background:rgba(255,255,255,.22);
}

#mapInfo{
margin-top:15px;
padding:20px;
border-radius:18px;
background:rgba(255,255,255,.1);
text-align:center;
}

footer{
text-align:center;
padding:30px;
opacity:.6;
}

.loading{
opacity:.7;
}

@media(max-width:700px){
.details{
grid-template-columns:repeat(2,1fr);
}

.maps{
grid-template-columns:1fr;
}

.temp{
font-size:55px;
}

header h1{
font-size:28px;
}
}
</style>
</head>

<body>

<header>
<h1>🇬🇷 Greece Weather</h1>
<p>15ήμερη πολυμοντελική πρόγνωση καιρού για την Ελλάδα</p>
</header>

<div class="container">

<div class="search">
<input id="searchInput" placeholder="Αναζήτηση πόλης ή περιοχής...">
<button onclick="searchLocation()">🔎 Αναζήτηση</button>
</div>

<h2 class="section-title">🏙️ Μεγάλες πόλεις</h2>

<div class="cities">

<button class="city-button" onclick="loadCity('Αθήνα',37.9838,23.7275)">Αθήνα</button>

<button class="city-button" onclick="loadCity('Θεσσαλονίκη',40.6401,22.9444)">Θεσσαλονίκη</button>

<button class="city-button" onclick="loadCity('Πάτρα',38.2466,21.7346)">Πάτρα</button>

<button class="city-button" onclick="loadCity('Ηράκλειο',35.3387,25.1442)">Ηράκλειο</button>

<button class="city-button" onclick="loadCity('Λάρισα',39.6390,22.4191)">Λάρισα</button>

<button class="city-button" onclick="loadCity('Βόλος',39.3610,22.9425)">Βόλος</button>

<button class="city-button" onclick="loadCity('Ιωάννινα',39.6650,20.8537)">Ιωάννινα</button>

<button class="city-button" onclick="loadCity('Καβάλα',40.9396,24.4018)">Καβάλα</button>

<button class="city-button" onclick="loadCity('Ρόδος',36.4349,28.2176)">Ρόδος</button>

<button class="city-button" onclick="loadCity('Χανιά',35.5138,24.0180)">Χανιά</button>

</div>

<h2 class="section-title">📍 Περισσότερες περιοχές</h2>

<div class="cities">

<button class="city-button" onclick="loadCity('Κοζάνη',40.3007,21.7890)">Κοζάνη</button>

<button class="city-button" onclick="loadCity('Τρίκαλα',39.5550,21.7687)">Τρίκαλα</button>

<button class="city-button" onclick="loadCity('Σέρρες',41.0856,23.5497)">Σέρρες</button>

<button class="city-button" onclick="loadCity('Αλεξανδρούπολη',40.8457,25.8744)">Αλεξανδρούπολη</button>

<button class="city-button" onclick="loadCity('Κατερίνη',40.2719,22.5025)">Κατερίνη</button>

<button class="city-button" onclick="loadCity('Λαμία',38.9000,22.4333)">Λαμία</button>

<button class="city-button" onclick="loadCity('Χαλκίδα',38.4636,23.5994)">Χαλκίδα</button>

<button class="city-button" onclick="loadCity('Καλαμάτα',37.0391,22.1127)">Καλαμάτα</button>

<button class="city-button" onclick="loadCity('Κόρινθος',37.9400,22.9513)">Κόρινθος</button>

<button class="city-button" onclick="loadCity('Μυτιλήνη',39.1000,26.5500)">Μυτιλήνη</button>

</div>

<section class="current">

<h2 id="cityName">Θεσσαλονίκη</h2>

<div class="temp" id="currentTemp">--°</div>

<div class="status" id="currentStatus">
Φόρτωση πραγματικών δεδομένων...
</div>

<div class="details">

<div class="detail">
🌡️ Αίσθηση<br>
<b id="feels">--°</b>
</div>

<div class="detail">
💧 Υγρασία<br>
<b id="humidity">--%</b>
</div>

<div class="detail">
💨 Άνεμος<br>
<b id="wind">-- km/h</b>
</div>

<div class="detail">
🌧️ Βροχή<br>
<b id="rainNow">-- mm</b>
</div>

</div>

</section>

<h2 class="section-title">📅 15ήμερη πρόγνωση</h2>

<div id="forecast" class="forecast">
<div class="loading">Φόρτωση πρόγνωσης...</div>
</div>

<div class="models">
<b>📊 Πώς υπολογίζεται:</b><br>
Η πρόγνωση βασίζεται σε ensemble mean δεδομένα και, όπου υπάρχει διαθέσιμος
ορίζοντας, συνδυάζει πολλαπλές ensemble πηγές. Για το πλήρες 15ήμερο
χρησιμοποιούνται ιδιαίτερα τα ECMWF IFS και ECMWF AIFS ensemble δεδομένα.
Η μέση τιμή δεν σημαίνει ότι η πρόγνωση είναι βέβαιη — η αβεβαιότητα αυξάνεται
όσο προχωράμε προς την 15η ημέρα.
</div>

<h2 class="section-title">🗺️ Καιρικοί χάρτες</h2>

<div class="maps">

<button class="mapbutton" onclick="mapMessage('🌡️','Θερμοκρασία 850 hPa')">
🌡️ Θερμοκρασία 850 hPa
</button>

<button class="mapbutton" onclick="mapMessage('🌧️','Βροχή και χιόνι')">
🌧️ Βροχή / Χιόνι
</button>

<button class="mapbutton" onclick="mapMessage('💨','Άνεμος')">
💨 Άνεμος
</button>

</div>

<div id="mapInfo">
Επίλεξε έναν χάρτη.
</div>

</div>

<footer>
Greece Weather © 2026
</footer>

<script>

let currentLat = 40.6401;
let currentLon = 22.9444;
let currentCity = "Θεσσαλονίκη";


function loadCity(name,lat,lon){

currentCity=name;
currentLat=lat;
currentLon=lon;

document.getElementById("cityName").textContent=name;

getWeather();

window.scrollTo({
top:document.querySelector(".current").offsetTop-10,
behavior:"smooth"
});

}


async function getWeather(){

document.getElementById("forecast").innerHTML=
"<div class='loading'>⏳ Φόρτωση 15ήμερης πολυμοντελικής πρόγνωσης...</div>";

try{

/*
ECMWF IFS + ECMWF AIFS ensemble means.
Και τα δύο είναι διαθέσιμα μέχρι 15 ημέρες.
*/

const url =
"https://ensemble-api.open-meteo.com/v1/ensemble"+
"?latitude="+currentLat+
"&longitude="+currentLon+
"&models=ecmwf_ifs025,ecmwf_aifs025"+
"&hourly=temperature_2m"+
"&daily=temperature_2m_max,temperature_2m_min,precipitation_sum"+
"&forecast_days=15"+
"&timezone=auto";

const response=await fetch(url);

if(!response.ok)
throw new Error("API error");

const data=await response.json();


/*
Τα ensemble means επιστρέφονται ως arrays.
Ο κώδικας βρίσκει αυτόματα τα διαθέσιμα
model fields και υπολογίζει τον μέσο όρο.
*/

const daily=data.daily;

let maxKeys=Object.keys(daily)
.filter(k=>k.includes("temperature_2m_max"));

let minKeys=Object.keys(daily)
.filter(k=>k.includes("temperature_2m_min"));

let rainKeys=Object.keys(daily)
.filter(k=>k.includes("precipitation_sum"));


let maxValues=averageArrays(
maxKeys.map(k=>daily[k])
);

let minValues=averageArrays(
minKeys.map(k=>daily[k])
);

let rainValues=averageArrays(
rainKeys.map(k=>daily[k])
);


const forecast=document.getElementById("forecast");

forecast.innerHTML="";


for(let i=0;i<15;i++){

const date=new Date(daily.time[i]);

const day=date.toLocaleDateString("el-GR",{
weekday:"short"
});

const dateText=
date.getDate()+"/"+(date.getMonth()+1);

const max=
Math.round(maxValues[i]);

const min=
Math.round(minValues[i]);

const rain=
rainValues[i] != null ?
rainValues[i].toFixed(1) :
"0.0";

const icon=
rain>2 ? "🌧️" :
rain>0.2 ? "🌦️" :
"☀️";


forecast.innerHTML+=`

<div class="day">

<div class="date">
${day} ${dateText}
</div>

<div class="icon">
${icon}
</div>

<div class="max">
${max}°
</div>

<div class="min">
${min}°
</div>

<div class="rain">
🌧️ ${rain} mm
</div>

</div>

`;

}


/*
Τρέχουσα θερμοκρασία:
χρησιμοποιούμε το κανονικό ECMWF IFS
για την τρέχουσα συνθήκη.
*/

await getCurrentWeather();

}
catch(error){

console.error(error);

document.getElementById("forecast").innerHTML=`

<div style="
background:rgba(255,80,80,.15);
padding:20px;
border-radius:15px;
">

❌ Δεν ήταν δυνατή η φόρτωση των δεδομένων.
<br><br>
Δοκίμασε ξανά σε λίγα δευτερόλεπτα.

</div>

`;

}

}


function averageArrays(arrays){

if(!arrays.length)
return [];

const length=Math.max(
...arrays.map(a=>a.length)
);

const result=[];

for(let i=0;i<length;i++){

let values=[];

for(const arr of arrays){

if(arr && arr[i] !== null && arr[i] !== undefined){
values.push(Number(arr[i]));
}

}

result.push(
values.length ?
values.reduce((a,b)=>a+b,0)/values.length :
null
);

}

return result;

}


async function getCurrentWeather(){

try{

const url=
"https://api.open-meteo.com/v1/forecast"+
"?latitude="+currentLat+
"&longitude="+currentLon+
"&current=temperature_2m,relative_humidity_2m,apparent_temperature,wind_speed_10m,precipitation"+
"&timezone=auto"+
"&forecast_days=1";

const response=await fetch(url);

const data=await response.json();

const c=data.current;

document.getElementById("currentTemp").textContent=
Math.round(c.temperature_2m)+"°C";

document.getElementById("feels").textContent=
Math.round(c.apparent_temperature)+"°C";

document.getElementById("humidity").textContent=
c.relative_humidity_2m+"%";

document.getElementById("wind").textContent=
Math.round(c.wind_speed_10m)+" km/h";

document.getElementById("rainNow").textContent=
c.precipitation+" mm";

document.getElementById("currentStatus").textContent=
"Πραγματικά δεδομένα πρόγνωσης για "+currentCity;

}
catch(e){

document.getElementById("currentStatus").textContent=
"Δεν φορτώθηκαν τα τρέχοντα δεδομένα.";

}

}


async function searchLocation(){

const input=
document.getElementById("searchInput").value.trim();

if(!input)
return;

try{

const url=
"https://geocoding-api.open-meteo.com/v1/search"+
"?name="+encodeURIComponent(input)+
"&count=1"+
"&language=el"+
"&format=json";

const response=await fetch(url);

const data=await response.json();

if(!data.results || !data.results.length){

alert("Δεν βρέθηκε η περιοχή.");

return;

}

const place=data.results[0];

loadCity(
place.name,
place.latitude,
place.longitude
);

}
catch(e){

alert("Δεν ήταν δυνατή η αναζήτηση.");

}

}


function mapMessage(icon,title){

document.getElementById("mapInfo").innerHTML=`

<div style="font-size:35px">
${icon}
</div>

<h3 style="margin:10px">
${title}
</h3>

<p style="opacity:.8">
Ο χάρτης θα χρησιμοποιεί πραγματικά δεδομένα
καιρικών μοντέλων της Ελλάδας.
</p>

`;

}


document.getElementById("searchInput")
.addEventListener("keydown",function(e){

if(e.key==="Enter")
searchLocation();

});


getWeather();

</script>

</body>
</html>
