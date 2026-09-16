<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<link rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

<style>

*{
  box-sizing:border-box;
}

body{
  margin:0;
  font-family:Arial,sans-serif;
  background:linear-gradient(180deg,#071b2d,#0d304b);
  color:white;
}

header{
  text-align:center;
  padding:28px 15px;
  background:rgba(0,0,0,.25);
}

header h1{
  margin:0;
  font-size:30px;
}

header p{
  margin:8px 0 0;
  opacity:.8;
}

.container{
  max-width:1100px;
  margin:auto;
  padding:20px;
}

.search{
  display:flex;
  gap:10px;
  margin-bottom:25px;
}

.search input{
  flex:1;
  min-width:0;
  padding:14px;
  border:0;
  border-radius:12px;
  font-size:16px;
}

.search button{
  border:0;
  border-radius:12px;
  padding:0 20px;
  background:#2196f3;
  color:white;
  font-size:16px;
}

.section-title{
  font-size:20px;
  font-weight:bold;
  margin:25px 0 12px;
}

.city-buttons{
  display:flex;
  flex-wrap:wrap;
  gap:8px;
}

.city-buttons button{
  border:0;
  border-radius:10px;
  padding:10px 14px;
  background:#173d5c;
  color:white;
  cursor:pointer;
}

.current{
  margin-top:25px;
  padding:22px;
  border-radius:18px;
  background:rgba(255,255,255,.09);
}

.city-name{
  font-size:28px;
  font-weight:bold;
}

.temp{
  font-size:52px;
  font-weight:bold;
  margin:10px 0;
}

.status{
  opacity:.9;
  font-size:18px;
}

.forecast{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(135px,1fr));
  gap:10px;
  margin-top:15px;
}

.day{
  padding:15px;
  border-radius:15px;
  background:rgba(255,255,255,.09);
  text-align:center;
}

.day-date{
  font-weight:bold;
  margin-bottom:8px;
}

.weather-icon{
  font-size:34px;
  margin:6px 0;
}

.weather-text{
  font-size:14px;
  min-height:34px;
  opacity:.9;
}

.max{
  font-size:23px;
  font-weight:bold;
  margin-top:7px;
}

.min{
  margin-top:5px;
  opacity:.7;
}

.rain{
  margin-top:9px;
  font-size:14px;
  color:#a8ddff;
}

.snow{
  margin-top:4px;
  font-size:14px;
  color:#e8f7ff;
}

.loading{
  text-align:center;
  padding:25px;
  opacity:.8;
}

.error{
  background:#812525;
  border-radius:12px;
  padding:15px;
}

#weatherMap{
  width:100%;
  height:350px;
  margin-top:15px;
  border-radius:18px;
  overflow:hidden;
}

footer{
  text-align:center;
  padding:30px;
  opacity:.6;
  font-size:13px;
}

</style>
</head>

<body>

<header>

<h1>🌦️ Greece Weather</h1>

<p>Πρόγνωση καιρού για όλο τον κόσμο</p>

</header>


<div class="container">


<!-- SEARCH -->

<div class="search">

<input
id="searchInput"
type="text"
placeholder="Αναζήτησε πόλη ή περιοχή..."
>

<button id="searchButton">
Αναζήτηση
</button>

</div>


<!-- CITIES -->

<div class="section-title">
Μεγάλες πόλεις
</div>

<div class="city-buttons">

<button data-name="Αθήνα" data-lat="37.9838" data-lon="23.7275">Αθήνα</button>

<button data-name="Θεσσαλονίκη" data-lat="40.6401" data-lon="22.9444">Θεσσαλονίκη</button>

<button data-name="Πάτρα" data-lat="38.2466" data-lon="21.7346">Πάτρα</button>

<button data-name="Ηράκλειο" data-lat="35.3387" data-lon="25.1442">Ηράκλειο</button>

<button data-name="Λάρισα" data-lat="39.6390" data-lon="22.4191">Λάρισα</button>

<button data-name="Βόλος" data-lat="39.3610" data-lon="22.9425">Βόλος</button>

<button data-name="Ιωάννινα" data-lat="39.6650" data-lon="20.8537">Ιωάννινα</button>

<button data-name="Καβάλα" data-lat="40.9396" data-lon="24.4018">Καβάλα</button>

<button data-name="Ρόδος" data-lat="36.4349" data-lon="28.2176">Ρόδος</button>

<button data-name="Χανιά" data-lat="35.5138" data-lon="24.0180">Χανιά</button>

</div>


<div class="section-title">
Άλλες περιοχές
</div>

<div class="city-buttons">

<button data-name="Κοζάνη" data-lat="40.3007" data-lon="21.7889">Κοζάνη</button>

<button data-name="Τρίκαλα" data-lat="39.5556" data-lon="21.7675">Τρίκαλα</button>

<button data-name="Σέρρες" data-lat="41.0856" data-lon="23.5483">Σέρρες</button>

<button data-name="Αλεξανδρούπολη" data-lat="40.8457" data-lon="25.8739">Αλεξανδρούπολη</button>

<button data-name="Κατερίνη" data-lat="40.2726" data-lon="22.5025">Κατερίνη</button>

<button data-name="Λαμία" data-lat="38.9000" data-lon="22.4340">Λαμία</button>

<button data-name="Χαλκίδα" data-lat="38.4635" data-lon="23.5994">Χαλκίδα</button>

<button data-name="Καλαμάτα" data-lat="37.0390" data-lon="22.1142">Καλαμάτα</button>

<button data-name="Μυτιλήνη" data-lat="39.1067" data-lon="26.5547">Μυτιλήνη</button>

<button data-name="Κόρινθος" data-lat="37.9386" data-lon="22.9322">Κόρινθος</button>

</div>


<!-- CURRENT -->

<div class="current">

<div class="city-name" id="cityName">
Θεσσαλονίκη
</div>

<div class="temp" id="currentTemp">
--
</div>

<div class="status" id="currentStatus">
Φόρτωση...
</div>

</div>


<!-- 15 DAY -->

<div class="section-title">
15ήμερη πρόγνωση
</div>

<div id="forecast" class="forecast">

<div class="loading">
Φόρτωση πρόγνωσης...
</div>

</div>


<!-- MAP -->

<div class="section-title">
Τοποθεσία
</div>

<div id="weatherMap"></div>


</div>


<footer>
Δεδομένα: Open-Meteo / ECMWF
</footer>


<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>


<script>

/* =====================================
   SELECTED LOCATION
===================================== */

let selectedCity = {

name:"Θεσσαλονίκη",

lat:40.6401,

lon:22.9444

};


/* =====================================
   MAP
===================================== */

let map;

let marker;


function startMap(){

map = L.map("weatherMap")
.setView(
[
selectedCity.lat,
selectedCity.lon
],
9
);


L.tileLayer(
"https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
{
maxZoom:18,
attribution:"© OpenStreetMap"
}
).addTo(map);


marker = L.marker(
[
selectedCity.lat,
selectedCity.lon
]
)
.addTo(map)
.bindPopup(selectedCity.name)
.openPopup();

}


function updateMap(){

marker
.setLatLng(
[
selectedCity.lat,
selectedCity.lon
]
)
.bindPopup(selectedCity.name)
.openPopup();


map.setView(
[
selectedCity.lat,
selectedCity.lon
],
10
);

}


/* =====================================
   SELECT CITY
===================================== */

function selectCity(name,lat,lon){

selectedCity={

name:name,

lat:Number(lat),

lon:Number(lon)

};


document
.getElementById("cityName")
.textContent=name;


updateMap();

loadCurrentWeather();

loadForecast();

}


/* =====================================
   CITY BUTTONS
===================================== */

document
.querySelectorAll(".city-buttons button")
.forEach(button=>{

button.addEventListener(
"click",
()=>{

selectCity(

button.dataset.name,

button.dataset.lat,

button.dataset.lon

);

});

});


/* =====================================
   CURRENT WEATHER
===================================== */

async function loadCurrentWeather(){

const temp=
document.getElementById("currentTemp");

const status=
document.getElementById("currentStatus");


temp.textContent="--";

status.textContent="Φόρτωση...";


const url=

"https://api.open-meteo.com/v1/forecast"+

"?latitude="+selectedCity.lat+

"&longitude="+selectedCity.lon+

"&current=temperature_2m,weather_code,rain,snowfall,precipitation"+

"&timezone=auto";


try{

const response=
await fetch(
url,
{cache:"no-store"}
);


if(!response.ok)
throw new Error("API error");


const data=
await response.json();


const current=
data.current;


temp.textContent=
Math.round(
current.temperature_2m
)+"°C";


status.textContent=
getWeatherDescription(
current.weather_code,
current.snowfall,
current.rain,
current.precipitation
);

}

catch(error){

console.error(error);

status.textContent=
"Δεν ήταν δυνατή η φόρτωση.";

}

}


/* =====================================
   WEATHER DESCRIPTION
   WMO CODES
===================================== */

function getWeatherDescription(
code,
snowfall=0,
rain=0,
precipitation=0
){

/*
0
*/

if(code===0)
return "☀️ Αίθριος";


/*
1
*/

if(code===1)
return "🌤️ Κυρίως αίθριος";


/*
2
*/

if(code===2)
return "⛅ Μερική συννεφιά";


/*
3
*/

if(code===3)
return "☁️ Συννεφιά";


/*
45-48
*/

if(code===45 || code===48)
return "🌫️ Ομίχλη";


/*
51-53
*/

if(code>=51 && code<=53)
return "🌦️ Ψιλόβροχο";


/*
55
*/

if(code===55)
return "🌧️ Έντονο ψιλόβροχο";


/*
56-57
*/

if(code===56 || code===57)
return "🌧️ Παγωμένο ψιλόβροχο";


/*
61
*/

if(code===61)
return "🌧️ Ελαφριά βροχή";


/*
63
*/

if(code===63)
return "🌧️ Βροχή";


/*
65
*/

if(code===65)
return "🌧️ Ισχυρή βροχή";


/*
66-67
*/

if(code===66 || code===67)
return "🌧️ Παγωμένη βροχή";


/*
71
*/

if(code===71)
return "🌨️ Ελαφριά χιονόπτωση";


/*
73
*/

if(code===73)
return "❄️ Χιονόπτωση";


/*
75
*/

if(code===75)
return "❄️ Ισχυρή χιονόπτωση";


/*
77
*/

if(code===77)
return "❄️ Κόκκοι χιονιού";


/*
80
*/

if(code===80)
return "🌦️ Ελαφριές μπόρες";


/*
81
*/

if(code===81)
return "🌧️ Μπόρες";


/*
82
*/

if(code===82)
return "🌧️ Ισχυρές μπόρες";


/*
85
*/

if(code===85)
return "🌨️ Ελαφριές μπόρες χιονιού";


/*
86
*/

if(code===86)
return "❄️ Ισχυρές μπόρες χιονιού";


/*
95
*/

if(code===95)
return "⛈️ Καταιγίδα";


/*
96
*/

if(code===96)
return "⛈️ Καταιγίδα με χαλάζι";


/*
99
*/

if(code===99)
return "⛈️ Ισχυρή καταιγίδα με χαλάζι";


/*
FALLBACK

Αν υπάρχει snowfall αλλά
ο κωδικός δεν περιγράφει σωστά
την κατάσταση, κρατάμε χιόνι.
*/

if(Number(snowfall)>0)
return "❄️ Χιονόπτωση";


if(Number(rain)>0)
return "🌧️ Βροχή";


if(Number(precipitation)>0)
return "🌦️ Υετός";


return "☁️ Συννεφιά";

}


/* =====================================
   MODEL FORECAST
===================================== */

async function getModelForecast(model){

const url=

"https://api.open-meteo.com/v1/forecast"+

"?latitude="+selectedCity.lat+

"&longitude="+selectedCity.lon+

"&models="+model+

"&daily="+

"temperature_2m_max,"+
"temperature_2m_min,"+
"precipitation_sum,"+
"rain_sum,"+
"snowfall_sum,"+
"weather_code"+

"&forecast_days=15"+

"&timezone=auto";


const response=
await fetch(
url,
{cache:"no-store"}
);


if(!response.ok)
throw new Error(model+" error");


const data=
await response.json();


if(
data.error ||
!data.daily
){

throw new Error(
model+" no data"
);

}


return data.daily;

}


/* =====================================
   15 DAY FORECAST
===================================== */

async function loadForecast(){

const box=
document.getElementById("forecast");


box.innerHTML=
'<div class="loading">Φόρτωση 15ήμερης πρόγνωσης...</div>';


try{

const [ifs,aifs]=
await Promise.all([

getModelForecast(
"ecmwf_ifs025"
),

getModelForecast(
"ecmwf_aifs025"
)

]);


const days=
Math.min(
15,
ifs.time.length,
aifs.time.length
);


let html="";


for(
let i=0;
i<days;
i++
){

/*
TEMPERATURE
*/

const maxTemp=
(
Number(ifs.temperature_2m_max[i])+
Number(aifs.temperature_2m_max[i])
)/2;


const minTemp=
(
Number(ifs.temperature_2m_min[i])+
Number(aifs.temperature_2m_min[i])
)/2;


/*
RAIN
*/

const rain=
(
Number(ifs.rain_sum[i])+
Number(aifs.rain_sum[i])
)/2;


/*
SNOW
*/

const snow=
(
Number(ifs.snowfall_sum[i])+
Number(aifs.snowfall_sum[i])
)/2;


/*
PRECIPITATION
*/

const precipitation=
(
Number(ifs.precipitation_sum[i])+
Number(aifs.precipitation_sum[i])
)/2;


/*
WEATHER CODE

Χρησιμοποιούμε το πιο
"έντονο" από τα δύο μοντέλα.
*/

const code1=
Number(ifs.weather_code[i]);

const code2=
Number(aifs.weather_code[i]);


/*
SNOW HAS PRIORITY

Αν οποιοδήποτε μοντέλο
δίνει χιονόπτωση,
δεν θα εμφανίσουμε απλά
"βροχή".
*/

let finalCode;


if(snow>0){

if(snow<1)
finalCode=71;

else if(snow<4)
finalCode=73;

else
finalCode=75;

}

else if(rain>0){

if(rain<2)
finalCode=61;

else if(rain<8)
finalCode=63;

else
finalCode=65;

}

else{

finalCode=
Math.max(code1,code2);

}


/*
DATE
*/

const date=
new Date(
ifs.time[i]+"T12:00:00"
);


const dateText=
date.toLocaleDateString(
"el-GR",
{
weekday:"short",
day:"numeric",
month:"short"
}
);


/*
ICON + TEXT
*/

const weather=
getWeatherDescription(
finalCode,
snow,
rain,
precipitation
);


/*
EXTRACT ICON

*/

const icon=
weather.substring(
0,
2
);


const text=
weather.substring(
2
).trim();


/*
CARD
*/

html+=`

<div class="day">

<div class="day-date">
${dateText}
</div>

<div class="weather-icon">
${icon}
</div>

<div class="weather-text">
${text}
</div>

<div class="max">
${Math.round(maxTemp)}°C
</div>

<div class="min">
Ελάχιστη ${Math.round(minTemp)}°C
</div>

<div class="rain">
🌧️ ${rain.toFixed(1)} mm
</div>

<div class="snow">
❄️ ${snow.toFixed(1)} cm
</div>

</div>

`;

}


box.innerHTML=html;

}

catch(error){

console.error(
"FORECAST ERROR:",
error
);


box.innerHTML=`

<div class="error">

❌ Δεν φορτώθηκε η πρόγνωση.

<br><br>

Γίνεται νέα προσπάθεια...

</div>

`;


setTimeout(
loadForecast,
5000
);

}

}


/* =====================================
   SEARCH
===================================== */

async function searchPlace(){

const input=
document.getElementById(
"searchInput"
);


const query=
input.value.trim();


if(!query)
return;


const button=
document.getElementById(
"searchButton"
);


button.textContent="...";


try{

const url=

"https://geocoding-api.open-meteo.com/v1/search"+

"?name="+
encodeURIComponent(query)+

"&count=1"+

"&language=el"+

"&format=json";


const response=
await fetch(
url,
{cache:"no-store"}
);


if(!response.ok)
throw new Error("Search error");


const data=
await response.json();


if(
!data.results ||
data.results.length===0
){

alert(
"Δεν βρέθηκε η περιοχή."
);

return;

}


const place=
data.results[0];


selectCity(

place.name,

place.latitude,

place.longitude

);


input.value="";


}

catch(error){

console.error(error);

alert(
"Δεν ήταν δυνατή η αναζήτηση αυτή τη στιγμή."
);

}

finally{

button.textContent=
"Αναζήτηση";

}

}


/* =====================================
   SEARCH BUTTON
===================================== */

document
.getElementById("searchButton")
.addEventListener(
"click",
searchPlace
);


/* =====================================
   ENTER
===================================== */

document
.getElementById("searchInput")
.addEventListener(
"keydown",
event=>{

if(event.key==="Enter")
searchPlace();

});


/* =====================================
   START
===================================== */

startMap();

loadCurrentWeather();

loadForecast();

</script>

</body>
</html>
