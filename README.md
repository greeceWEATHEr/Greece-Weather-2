<!DOCTYPE html>
<html lang="el">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">

<title>Greece Weather</title>

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

/* ΑΠΛΟΣ ΧΑΡΤΗΣ */

#weatherMap{
height:450px;
width:100%;
border-radius:20px;
overflow:hidden;
box-shadow:0 10px 30px rgba(0,0,0,.35);
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
height:400px;
}

}

</style>

</head>

<body>

<header>

<h1>🇬🇷 Greece Weather</h1>

<p>
15ήμερη πρόγνωση για πολλές περιοχές της Ελλάδας
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

<h2 class="title">
🏙️ Μεγάλες πόλεις
</h2>

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


<!-- ΠΕΡΙΣΣΟΤΕΡΕΣ ΠΕΡΙΟΧΕΣ -->

<h2 class="title">
📍 Περισσότερες περιοχές
</h2>

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

<h2 id="cityName">
Θεσσαλονίκη
</h2>

<div
class="temperature"
id="currentTemp">
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
📅 15ήμερη πρόγνωση
</h2>

<div
id="forecast"
class="forecast">

Φόρτωση...

</div>


<div class="info">

<b>📊 Πρόγνωση</b><br>

Οι θερμοκρασίες και ο υετός βασίζονται σε
ensemble δεδομένα από ECMWF IFS και AIFS.
Η αβεβαιότητα αυξάνεται όσο προχωράμε
προς την 15η ημέρα.

</div>


<!-- ΑΠΛΟΣ ΧΑΡΤΗΣ -->

<h2 class="title">
🗺️ Τοποθεσία
</h2>

<div id="weatherMap"></div>


</div>


<footer>

Greece Weather © 2026

</footer>


<script
src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js">
</script>


<script>

/* =====================================================
   ΒΑΣΙΚΕΣ ΜΕΤΑΒΛΗΤΕΣ
===================================================== */

let cityName="Θεσσαλονίκη";

let latitude=40.6401;

let longitude=22.9444;


/* =====================================================
   ΧΑΡΤΗΣ
===================================================== */

const map=L.map("weatherMap")
.setView(
[latitude,longitude],
7
);


L.tileLayer(
"https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
{
maxZoom:18,
attribution:"© OpenStreetMap"
}
).addTo(map);


/* ΣΗΜΕΙΟ */

let cityMarker=L.marker(
[latitude,longitude]
)
.addTo(map)
.bindPopup(cityName)
.openPopup();


/* =====================================================
   ΑΛΛΑΓΗ ΠΟΛΗΣ
===================================================== */

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


/* Αλλάζει το σημείο στον χάρτη */

cityMarker
.setLatLng([lat,lon])
.bindPopup(name)
.openPopup();


/* Μετακινεί τον χάρτη στην περιοχή */

map.setView(
[lat,lon],
10
);


loadWeather();

}


/* =====================================================
   ΠΡΟΓΝΩΣΗ
===================================================== */

async function loadWeather(){

document.getElementById(
"forecast"
).innerHTML=
"⏳ Φόρτωση πρόγνωσης...";


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


const maxKeys=
Object.keys(d)
.filter(
key=>key.includes(
"temperature_2m_max"
)
);


const minKeys=
Object.keys(d)
.filter(
key=>key.includes(
"temperature_2m_min"
)
);


const rainKeys=
Object.keys(d)
.filter(
key=>key.includes(
"precipitation_sum"
)
);


const max=
averageArrays(
maxKeys.map(
key=>d[key]
)
);


const min=
averageArrays(
minKeys.map(
key=>d[key]
)
);


const rain=
averageArrays(
rainKeys.map(
key=>d[key]
)
);


let html="";


for(
let i=0;
i<15;
i++
){

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


if(rain[i]>5)
icon="🌧️";

else if(rain[i]>0.2)
icon="🌦️";


html+=`

<div class="day">

<b>
${weekday}
${date.getDate()}/${date.getMonth()+1}
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
"❌ Πρόβλημα φόρτωσης πρόγνωσης.";

}

}


/* =====================================================
   ΜΕΣΟΣ ΟΡΟΣ
===================================================== */

function averageArrays(arrays){

if(!arrays.length)
return [];


const length=
Math.max(
...arrays.map(
a=>a.length
)
);


const result=[];


for(
let i=0;
i<length;
i++
){

const values=[];


arrays.forEach(
arr=>{

if(
arr[i]!==null &&
arr[i]!==undefined &&
!isNaN(arr[i])
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


/* =====================================================
   ΤΡΕΧΩΝ ΚΑΙΡΟΣ
===================================================== */

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
Math.round(
c.temperature_2m
)+"°C";


document.getElementById(
"feels"
).textContent=
Math.round(
c.apparent_temperature
)+"°C";


document.getElementById(
"humidity"
).textContent=
c.relative_humidity_2m+"%";


document.getElementById(
"wind"
).textContent=
Math.round(
c.wind_speed_10m
)+" km/h";


document.getElementById(
"rainNow"
).textContent=
c.precipitation+" mm";


document.getElementById(
"condition"
).textContent=
"Πραγματικά δεδομένα για "+
cityName;

}
catch(error){

console.error(error);

}

}


/* =====================================================
   ΑΝΑΖΗΤΗΣΗ ΠΕΡΙΟΧΗΣ
===================================================== */

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

alert(
"Δεν βρέθηκε η περιοχή."
);

return;

}


const p=data.results[0];


loadCity(
p.name,
p.latitude,
p.longitude
);

}
catch(error){

alert(
"Δεν ήταν δυνατή η αναζήτηση."
);

}

}


/* =====================================================
   ENTER ΓΙΑ ΑΝΑΖΗΤΗΣΗ
===================================================== */

document.getElementById(
"searchInput"
).addEventListener(
"keydown",
function(e){

if(e.key==="Enter")
searchPlace();

}
);


/* =====================================================
   ΕΚΚΙΝΗΣΗ
===================================================== */

loadWeather();

</script>

</body>
</html>
