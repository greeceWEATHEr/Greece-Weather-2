<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">

<title>Greece Weather</title>

<!-- Leaflet για τον πραγματικό διαδραστικό χάρτη -->
<link
rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
/>

<style>

*{
box-sizing:border-box;
margin:0;
padding:0;
}

body{
font-family:Arial,sans-serif;
background:linear-gradient(160deg,#06172d,#0b4674,#071e38);
color:white;
min-height:100vh;
}

header{
text-align:center;
padding:32px 15px;
background:rgba(0,0,0,.22);
}

header h1{
font-size:34px;
margin-bottom:9px;
}

header p{
opacity:.85;
}

.container{
max-width:1200px;
margin:auto;
padding:20px 15px 50px;
}

.search{
display:flex;
gap:10px;
margin-bottom:25px;
}

.search input{
flex:1;
padding:15px;
border:0;
border-radius:13px;
font-size:16px;
}

.search button{
border:0;
border-radius:13px;
padding:0 20px;
font-weight:bold;
cursor:pointer;
}

.title{
font-size:24px;
margin:27px 0 15px;
}

.cities{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
gap:10px;
}

.city{
padding:15px 8px;
border:0;
border-radius:14px;
background:rgba(255,255,255,.12);
color:white;
cursor:pointer;
font-size:15px;
}

.city:hover{
background:rgba(255,255,255,.22);
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

.temperature{
font-size:64px;
font-weight:bold;
margin:12px;
}

.details{
display:grid;
grid-template-columns:repeat(4,1fr);
gap:10px;
margin-top:20px;
}

.detail{
background:rgba(0,0,0,.17);
padding:15px;
border-radius:14px;
}

.forecast{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
gap:12px;
}

.day{
background:rgba(255,255,255,.12);
padding:16px 8px;
border-radius:16px;
text-align:center;
}

.day .icon{
font-size:34px;
margin:9px;
}

.day .max{
font-size:23px;
font-weight:bold;
}

.day .min{
opacity:.65;
margin-top:5px;
}

.day .rain{
margin-top:9px;
font-size:13px;
}

.info{
margin-top:15px;
padding:16px;
border-radius:15px;
background:rgba(0,0,0,.17);
line-height:1.6;
font-size:14px;
}

.mapControls{
display:flex;
gap:8px;
flex-wrap:wrap;
margin-bottom:12px;
}

.mapControls button{
border:0;
border-radius:12px;
padding:13px 16px;
cursor:pointer;
font-weight:bold;
}

.mapControls button.active{
outline:3px solid rgba(255,255,255,.45);
}

.mapControls select{
border:0;
border-radius:12px;
padding:12px;
font-size:15px;
}

#weatherMap{
height:570px;
width:100%;
border-radius:20px;
overflow:hidden;
box-shadow:0 10px 30px rgba(0,0,0,.35);
}

.legend{
background:rgba(255,255,255,.95);
color:#111;
padding:10px;
border-radius:8px;
font-size:12px;
line-height:1.5;
}

.legendGradient{
width:180px;
height:13px;
margin:5px 0;
background:linear-gradient(
90deg,
#313695,
#4575b4,
#74add1,
#abd9e9,
#ffffbf,
#fdae61,
#f46d43,
#d73027
);
}

footer{
text-align:center;
padding:30px;
opacity:.55;
}

@media(max-width:700px){

.details{
grid-template-columns:repeat(2,1fr);
}

.temperature{
font-size:53px;
}

#weatherMap{
height:470px;
}

}

</style>
</head>

<body>

<header>

<h1>🇬🇷 Greece Weather</h1>

<p>
15ήμερη πολυμοντελική πρόγνωση για πολλές περιοχές της Ελλάδας
</p>

</header>

<div class="container">

<!-- ΑΝΑΖΗΤΗΣΗ -->

<div class="search">

<input
id="searchInput"
placeholder="Αναζήτηση πόλης ή περιοχής..."
>

<button onclick="searchPlace()">
🔎 Αναζήτηση
</button>

</div>


<!-- ΜΕΓΑΛΕΣ ΠΟΛΕΙΣ -->

<h2 class="title">🏙️ Μεγάλες πόλεις</h2>

<div class="cities">

<button class="city"
onclick="loadCity('Αθήνα',37.9838,23.7275)">
Αθήνα
</button>

<button class="city"
onclick="loadCity('Θεσσαλονίκη',40.6401,22.9444)">
Θεσσαλονίκη
</button>

<button class="city"
onclick="loadCity('Πάτρα',38.2466,21.7346)">
Πάτρα
</button>

<button class="city"
onclick="loadCity('Ηράκλειο',35.3387,25.1442)">
Ηράκλειο
</button>

<button class="city"
onclick="loadCity('Λάρισα',39.639,22.419)">
Λάρισα
</button>

<button class="city"
onclick="loadCity('Βόλος',39.361,22.9425)">
Βόλος
</button>

<button class="city"
onclick="loadCity('Ιωάννινα',39.665,20.8537)">
Ιωάννινα
</button>

<button class="city"
onclick="loadCity('Καβάλα',40.9396,24.4018)">
Καβάλα
</button>

<button class="city"
onclick="loadCity('Ρόδος',36.4349,28.2176)">
Ρόδος
</button>

<button class="city"
onclick="loadCity('Χανιά',35.5138,24.018)">
Χανιά
</button>

</div>


<!-- ΠΕΡΙΟΧΕΣ -->

<h2 class="title">📍 Περισσότερες περιοχές</h2>

<div class="cities">

<button class="city"
onclick="loadCity('Κοζάνη',40.3007,21.789)">
Κοζάνη
</button>

<button class="city"
onclick="loadCity('Τρίκαλα',39.555,21.7687)">
Τρίκαλα
</button>

<button class="city"
onclick="loadCity('Σέρρες',41.0856,23.5497)">
Σέρρες
</button>

<button class="city"
onclick="loadCity('Αλεξανδρούπολη',40.8457,25.8744)">
Αλεξανδρούπολη
</button>

<button class="city"
onclick="loadCity('Κατερίνη',40.2719,22.5025)">
Κατερίνη
</button>

<button class="city"
onclick="loadCity('Λαμία',38.9,22.4333)">
Λαμία
</button>

<button class="city"
onclick="loadCity('Χαλκίδα',38.4636,23.5994)">
Χαλκίδα
</button>

<button class="city"
onclick="loadCity('Καλαμάτα',37.0391,22.1127)">
Καλαμάτα
</button>

<button class="city"
onclick="loadCity('Μυτιλήνη',39.1,26.55)">
Μυτιλήνη
</button>

<button class="city"
onclick="loadCity('Κόρινθος',37.94,22.9513)">
Κόρινθος
</button>

</div>


<!-- ΤΡΕΧΩΝ ΚΑΙΡΟΣ -->

<section class="current">

<h2 id="cityName">Θεσσαλονίκη</h2>

<div class="temperature" id="currentTemp">
--
</div>

<div id="condition">
Φόρτωση...
</div>

<div class="details">

<div class="detail">
🌡️ Αίσθηση<br>
<b id="feels">--</b>
</div>

<div class="detail">
💧 Υγρασία<br>
<b id="humidity">--</b>
</div>

<div class="detail">
💨 Άνεμος<br>
<b id="wind">--</b>
</div>

<div class="detail">
🌧️ Υετός<br>
<b id="rainNow">--</b>
</div>

</div>

</section>


<!-- 15 ΗΜΕΡΕΣ -->

<h2 class="title">
📅 15ήμερη πολυμοντελική πρόγνωση
</h2>

<div id="forecast" class="forecast">

Φόρτωση...

</div>


<div class="info">

<b>📊 Πολυμοντελική πρόγνωση</b><br>

Η σελίδα χρησιμοποιεί ensemble mean δεδομένα από διαθέσιμα
καιρικά μοντέλα. Η μέση τιμή μειώνει την εξάρτηση από ένα μόνο
μοντέλο, αλλά η αβεβαιότητα αυξάνεται όσο προχωράμε προς την
15η ημέρα.

</div>


<!-- ΧΑΡΤΗΣ -->

<h2 class="title">
🗺️ Καιρικός χάρτης Ελλάδας
</h2>

<div class="mapControls">

<button id="tempBtn"
onclick="changeMap('temp')">
🌡️ 850 hPa
</button>

<button id="rainBtn"
onclick="changeMap('rain')">
🌧️ Βροχή / Χιόνι
</button>

<button id="windBtn"
onclick="changeMap('wind')">
💨 Άνεμος
</button>

<select id="mapDay"
onchange="loadMap()">

<option value="0">Σήμερα</option>
<option value="1">Αύριο</option>
<option value="2">+2 ημέρες</option>
<option value="3">+3 ημέρες</option>
<option value="4">+4 ημέρες</option>
<option value="5">+5 ημέρες</option>
<option value="6">+6 ημέρες</option>
<option value="7">+7 ημέρες</option>
<option value="8">+8 ημέρες</option>
<option value="9">+9 ημέρες</option>
<option value="10">+10 ημέρες</option>
<option value="11">+11 ημέρες</option>
<option value="12">+12 ημέρες</option>
<option value="13">+13 ημέρες</option>
<option value="14">+14 ημέρες</option>

</select>

</div>


<div id="weatherMap"></div>


<div id="mapDescription" class="info">
Φόρτωση χάρτη...
</div>

</div>


<footer>
Greece Weather © 2026
</footer>


<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

/* =========================
   ΒΑΣΙΚΕΣ ΜΕΤΑΒΛΗΤΕΣ
========================= */

let cityName="Θεσσαλονίκη";

let latitude=40.6401;

let longitude=22.9444;

let mapType="temp";

let map;


/* =========================
   ΧΑΡΤΗΣ
========================= */

map=L.map("weatherMap").setView(
[38.7,23.7],
6
);


/* Κανονικός χάρτης Ελλάδας */

L.tileLayer(
"https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
{
maxZoom:12,
attribution:"© OpenStreetMap"
}
).addTo(map);


/* =========================
   ΣΗΜΕΙΟ ΠΟΛΗΣ
========================= */

let cityMarker=L.marker(
[latitude,longitude]
)
.addTo(map)
.bindPopup(cityName)
.openPopup();


/* =========================
   GRID WEATHER CELLS
========================= */

let weatherCells=[];


/* Πλέγμα Ελλάδας */

const grid=[];

for(
let lat=34.5;
lat<=42.2;
lat+=0.35
){

for(
let lon=19.0;
lon<=29.8;
lon+=0.45
){

grid.push([
lat,
lon
]);

}

}


/* =========================
   ΕΠΙΛΟΓΗ ΤΥΠΟΥ ΧΑΡΤΗ
========================= */

function changeMap(type){

mapType=type;

document
.getElementById("tempBtn")
.classList.remove("active");

document
.getElementById("rainBtn")
.classList.remove("active");

document
.getElementById("windBtn")
.classList.remove("active");

if(type==="temp")
document.getElementById("tempBtn")
.classList.add("active");

if(type==="rain")
document.getElementById("rainBtn")
.classList.add("active");

if(type==="wind")
document.getElementById("windBtn")
.classList.add("active");

loadMap();

}


/* =========================
   ΧΡΩΜΑ ΘΕΡΜΟΚΡΑΣΙΑΣ
========================= */

function temperatureColor(t){

if(t<=-5)return "#313695";

if(t<=0)return "#4575b4";

if(t<=5)return "#74add1";

if(t<=10)return "#abd9e9";

if(t<=15)return "#ffffbf";

if(t<=20)return "#fee090";

if(t<=25)return "#fdae61";

if(t<=30)return "#f46d43";

return "#d73027";

}


/* =========================
   ΧΡΩΜΑ ΒΡΟΧΗΣ
========================= */

function rainColor(r){

if(r<=0.1)
return "transparent";

if(r<1)
return "#4da6ff";

if(r<5)
return "#2878ff";

if(r<10)
return "#4050d8";

if(r<20)
return "#713ac7";

if(r<40)
return "#9b20b5";

return "#c0009b";

}


/* =========================
   ΧΡΩΜΑ ΑΝΕΜΟΥ
========================= */

function windColor(w){

if(w<10)
return "#b8f3ff";

if(w<20)
return "#69d9ff";

if(w<30)
return "#27a9ff";

if(w<40)
return "#3268e8";

if(w<60)
return "#7048d8";

return "#a52ad1";

}


/* =========================
   ΦΟΡΤΩΣΗ MAP DATA
========================= */

async function loadMap(){

/* καθαρίζουμε παλιά cells */

weatherCells.forEach(
cell=>map.removeLayer(cell)
);

weatherCells=[];


const day=
Number(
document.getElementById("mapDay").value
);


/*
Πραγματικό grid forecast.
Για 850 hPa παίρνουμε θερμοκρασία περίπου
στα 1500 m.
*/

const lats=grid.map(x=>x[0]).join(",");

const lons=grid.map(x=>x[1]).join(",");


let hourlyVariables="";

if(mapType==="temp"){

hourlyVariables=
"temperature_850hPa";

}

if(mapType==="rain"){

hourlyVariables=
"precipitation";

}

if(mapType==="wind"){

hourlyVariables=
"wind_speed_10m";

}


const url=
"https://api.open-meteo.com/v1/forecast"+
"?latitude="+lats+
"&longitude="+lons+
"&hourly="+hourlyVariables+
"&forecast_days=15"+
"&timezone=Europe%2FAthens";


try{

const response=
await fetch(url);

const data=
await response.json();


/*
Για πολλά coordinates το API επιστρέφει
array από responses.
*/

const locations=
Array.isArray(data)
?data
:[data];


locations.forEach(
(location,index)=>{

if(!location.hourly)
return;

const lat=grid[index][0];

const lon=grid[index][1];

const times=
location.hourly.time;


/*
12:00 τοπική ώρα.
Έτσι ο ημερήσιος χάρτης είναι
πιο εύκολος στην ανάγνωση.
*/

let hourIndex=
day*24+12;

if(hourIndex>=times.length)
hourIndex=times.length-1;


let value;


if(mapType==="temp")
value=
location.hourly.temperature_850hPa[
hourIndex
];

if(mapType==="rain")
value=
location.hourly.precipitation[
hourIndex
];

if(mapType==="wind")
value=
location.hourly.wind_speed_10m[
hourIndex
];


if(value===undefined || value===null)
return;


/*
Κάθε grid cell είναι μικρό
ορθογώνιο πάνω στον πραγματικό χάρτη.
*/

const sizeLat=.34;

const sizeLon=.44;


let color;

let opacity=.52;


if(mapType==="temp")
color=temperatureColor(value);

if(mapType==="rain")
color=rainColor(value);

if(mapType==="wind")
color=windColor(value);


if(mapType==="rain" && value<=0.1)
return;


const rectangle=
L.rectangle(
[
[
lat-sizeLat/2,
lon-sizeLon/2
],
[
lat+sizeLat/2,
lon+sizeLon/2
]
],
{
stroke:false,
fillColor:color,
fillOpacity:opacity,
interactive:true
}
).addTo(map);


let unit="";

if(mapType==="temp")
unit="°C";

if(mapType==="rain")
unit=" mm";

if(mapType==="wind")
unit=" km/h";


rectangle.bindTooltip(
"<b>"+
value.toFixed(1)+
unit+
"</b>",
{
sticky:true
}
);


weatherCells.push(rectangle);

}
);


updateMapDescription();


}
catch(error){

console.error(error);

document.getElementById(
"mapDescription"
).innerHTML=
"❌ Δεν ήταν δυνατή η φόρτωση του χάρτη.";

}

}


/* =========================
   ΠΕΡΙΓΡΑΦΗ MAP
========================= */

function updateMapDescription(){

const day=
document.getElementById("mapDay")
.options[
document.getElementById("mapDay").selectedIndex
].text;


if(mapType==="temp"){

document.getElementById(
"mapDescription"
).innerHTML=

"🌡️ <b>Θερμοκρασία 850 hPa</b><br>"+
day+
"<br>Τα χρώματα δείχνουν τη θερμοκρασία "+
"της ατμοσφαιρικής στάθμης των 850 hPa (~1500 m).";

}

if(mapType==="rain"){

document.getElementById(
"mapDescription"
).innerHTML=

"🌧️ <b>Βροχή / Χιόνι</b><br>"+
day+
"<br>Μπλε = υετός. Όσο πιο μωβ, τόσο μεγαλύτερη η προβλεπόμενη ποσότητα.";

}

if(mapType==="wind"){

document.getElementById(
"mapDescription"
).innerHTML=

"💨 <b>Άνεμος</b><br>"+
day+
"<br>Τα χρώματα δείχνουν την ταχύτητα του ανέμου στα 10 m.";

}

}


/* =========================
   ΠΟΛΗ
========================= */

function loadCity(
name,
lat,
lon
){

cityName=name;

latitude=lat;

longitude=lon;


document.getElementById(
"cityName"
).textContent=name;


cityMarker
.setLatLng([lat,lon])
.bindPopup(name)
.openPopup();


map.setView(
[lat,lon],
7
);


loadWeather();

}


/* =========================
   ΠΡΟΓΝΩΣΗ ΠΟΛΗΣ
========================= */

async function loadWeather(){

document.getElementById(
"forecast"
).innerHTML=
"⏳ Φόρτωση πραγματικής πρόγνωσης...";


try{

const url=
"https://ensemble-api.open-meteo.com/v1/ensemble"+
"?latitude="+latitude+
"&longitude="+longitude+
"&models=ecmwf_ifs025,ecmwf_aifs025"+
"&daily=temperature_2m_max,temperature_2m_min,precipitation_sum"+
"&forecast_days=15"+
"&timezone=Europe%2FAthens";


const response=
await fetch(url);

const data=
await response.json();


const d=data.daily;


/*
Εντοπίζουμε αυτόματα τα model arrays.
*/

const maxKeys=
Object.keys(d)
.filter(
key=>key.includes("temperature_2m_max")
);

const minKeys=
Object.keys(d)
.filter(
key=>key.includes("temperature_2m_min")
);

const rainKeys=
Object.keys(d)
.filter(
key=>key.includes("precipitation_sum")
);


const max=
averageArrays(
maxKeys.map(key=>d[key])
);

const min=
averageArrays(
minKeys.map(key=>d[key])
);

const rain=
averageArrays(
rainKeys.map(key=>d[key])
);


let html="";


for(let i=0;i<15;i++){

const date=
new Date(d.time[i]);


const weekday=
date.toLocaleDateString(
"el-GR",
{
weekday:"short"
}
);


let icon="☀️";

if(rain[i]>2)
icon="🌧️";

else if(rain[i]>.2)
icon="🌦️";


html+=`

<div class="day">

<b>
${weekday} ${date.getDate()}/${date.getMonth()+1}
</b>

<div class="icon">
${icon}
</div>

<div class="max">
${Math.round(max[i])}°
</div>

<div class="min">
${Math.round(min[i])}°
</div>

<div class="rain">
🌧️ ${rain[i].toFixed(1)} mm
</div>

</div>

`;

}


document.getElementById(
"forecast"
).innerHTML=html;


await loadCurrent();


}
catch(error){

console.error(error);

document.getElementById(
"forecast"
).innerHTML=
"❌ Πρόβλημα φόρτωσης δεδομένων.";

}

}


/* =========================
   ΜΕΣΟΣ ΟΡΟΣ MODELS
========================= */

function averageArrays(arrays){

if(!arrays.length)
return [];

const length=
Math.max(
...arrays.map(a=>a.length)
);

const result=[];


for(let i=0;i<length;i++){

const values=[];


arrays.forEach(
arr=>{

if(
arr[i]!==null &&
arr[i]!==undefined
){

values.push(
Number(arr[i])
);

}

}
);


result.push(
values.length
?
values.reduce(
(a,b)=>a+b,
0
)/values.length
:null
);

}


return result;

}


/* =========================
   ΤΡΕΧΟΥΣΑ ΣΥΝΘΗΚΗ
========================= */

async function loadCurrent(){

try{

const url=
"https://api.open-meteo.com/v1/forecast"+
"?latitude="+latitude+
"&longitude="+longitude+
"&current=temperature_2m,relative_humidity_2m,apparent_temperature,wind_speed_10m,precipitation"+
"&timezone=Europe%2FAthens";


const response=
await fetch(url);

const data=
await response.json();


const c=data.current;


document.getElementById(
"currentTemp"
).textContent=
Math.round(c.temperature_2m)+"°C";


document.getElementById(
"feels"
).textContent=
Math.round(c.apparent_temperature)+"°C";


document.getElementById(
"humidity"
).textContent=
c.relative_humidity_2m+"%";


document.getElementById(
"wind"
).textContent=
Math.round(c.wind_speed_10m)+" km/h";


document.getElementById(
"rainNow"
).textContent=
c.precipitation+" mm";


document.getElementById(
"condition"
).textContent=
"Πραγματικά δεδομένα για "+cityName;

}
catch(e){}

}


/* =========================
   ΑΝΑΖΗΤΗΣΗ
========================= */

async function searchPlace(){

const text=
document.getElementById(
"searchInput"
).value.trim();


if(!text)
return;


try{

const url=
"https://geocoding-api.open-meteo.com/v1/search"+
"?name="+
encodeURIComponent(text)+
"&count=1"+
"&language=el"+
"&format=json";


const response=
await fetch(url);

const data=
await response.json();


if(
!data.results ||
!data.results.length
){

alert("Δεν βρέθηκε η περιοχή.");

return;

}


const p=data.results[0];


loadCity(
p.name,
p.latitude,
p.longitude
);


}
catch(e){

alert(
"Δεν ήταν δυνατή η αναζήτηση."
);

}

}


/* Enter για αναζήτηση */

document.getElementById(
"searchInput"
).addEventListener(
"keydown",
e=>{

if(e.key==="Enter")
searchPlace();

}
);


/* =========================
   ΕΚΚΙΝΗΣΗ
========================= */

document.getElementById(
"tempBtn"
).classList.add("active");


loadWeather();

loadMap();

</script>

</body>
</html>
