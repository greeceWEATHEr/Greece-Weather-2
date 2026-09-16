<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">

<title>The Greece Weather</title>

<link rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"/>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
}

body{
  font-family:Arial,sans-serif;
  min-height:100vh;
  color:white;
  background:
    radial-gradient(circle at top,#214d78 0%,#102b4b 35%,#06111f 100%);
}

.container{
  width:94%;
  max-width:1200px;
  margin:auto;
  padding:25px 0 50px;
}

header{
  text-align:center;
  margin-bottom:22px;
}

header h1{
  font-size:36px;
  margin-bottom:7px;
}

header p{
  color:#c5d8eb;
}

.search{
  display:flex;
  gap:10px;
  max-width:760px;
  margin:20px auto;
}

.search input{
  flex:1;
  padding:15px 17px;
  border:none;
  outline:none;
  border-radius:15px;
  font-size:16px;
}

.search button{
  border:none;
  border-radius:15px;
  padding:0 23px;
  background:#2389ff;
  color:white;
  font-size:16px;
  cursor:pointer;
}

.city-buttons{
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  gap:9px;
  margin-bottom:22px;
}

.city-buttons button{
  border:1px solid rgba(255,255,255,.16);
  background:rgba(255,255,255,.09);
  color:white;
  padding:10px 14px;
  border-radius:12px;
  cursor:pointer;
}

.card{
  background:rgba(255,255,255,.085);
  border:1px solid rgba(255,255,255,.12);
  border-radius:22px;
  padding:22px;
  margin-bottom:20px;
  backdrop-filter:blur(14px);
  box-shadow:0 15px 40px rgba(0,0,0,.2);
}

.current{
  text-align:center;
}

.location{
  font-size:28px;
  font-weight:bold;
}

.current-weather{
  display:flex;
  justify-content:center;
  align-items:center;
  gap:18px;
  margin-top:15px;
}

.current-icon{
  font-size:65px;
}

.current-temp{
  font-size:55px;
  font-weight:bold;
}

.condition{
  font-size:19px;
  color:#d3e3f3;
  margin-top:4px;
}

.section-title{
  font-size:24px;
  font-weight:bold;
  margin-bottom:15px;
}

.forecast{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(135px,1fr));
  gap:12px;
}

.day{
  background:rgba(0,0,0,.18);
  border-radius:17px;
  padding:15px 10px;
  text-align:center;
  min-height:190px;
}

.day-name{
  font-weight:bold;
  line-height:1.3;
}

.day-icon{
  font-size:43px;
  margin:9px 0;
}

.high{
  font-size:21px;
  font-weight:bold;
}

.low{
  font-size:16px;
  color:#bcd0e4;
  margin-top:4px;
}

.precip{
  color:#9ecbff;
  font-size:13px;
  margin-top:9px;
}

.status{
  text-align:center;
  color:#bfd2e5;
  margin:10px;
}

.error{
  text-align:center;
  color:#ff9d9d;
}

#map{
  width:100%;
  height:380px;
  border-radius:18px;
  overflow:hidden;
}

@media(max-width:600px){

  header h1{
    font-size:29px;
  }

  .search{
    flex-direction:column;
  }

  .search button{
    padding:13px;
  }

  .current-temp{
    font-size:46px;
  }

  .forecast{
    grid-template-columns:repeat(2,1fr);
  }
}
</style>
</head>

<body>

<div class="container">

<header>
  <h1>🌦️ The Greece Weather</h1>
  <p>Πρόγνωση καιρού με μοντέλα ECMWF</p>
</header>

<div class="search">
  <input
    id="searchInput"
    placeholder="Αναζήτησε πόλη ή περιοχή σε όλο τον κόσμο">
  <button onclick="searchLocation()">Αναζήτηση</button>
</div>

<div class="city-buttons">
  <button onclick="selectCity('Αθήνα',37.9838,23.7275)">Αθήνα</button>
  <button onclick="selectCity('Θεσσαλονίκη',40.6401,22.9444)">Θεσσαλονίκη</button>
  <button onclick="selectCity('Πάτρα',38.2466,21.7346)">Πάτρα</button>
  <button onclick="selectCity('Λάρισα',39.639,22.419)">Λάρισα</button>
  <button onclick="selectCity('Ηράκλειο',35.3387,25.1442)">Ηράκλειο</button>
  <button onclick="selectCity('Ιωάννινα',39.665,20.8537)">Ιωάννινα</button>
  <button onclick="selectCity('Καβάλα',40.9396,24.4018)">Καβάλα</button>
  <button onclick="selectCity('Ρόδος',36.4349,28.2176)">Ρόδος</button>
</div>

<div id="status" class="status"></div>

<div class="card current">

  <div id="locationName" class="location">
    Θεσσαλονίκη
  </div>

  <div class="current-weather">

    <div id="currentIcon" class="current-icon">
      🌤️
    </div>

    <div>
      <div id="currentTemp" class="current-temp">
        --°
      </div>

      <div id="currentCondition" class="condition">
        Φόρτωση...
      </div>
    </div>

  </div>

</div>

<div class="card">

  <div class="section-title">
    📅 Πρόγνωση 15 ημερών
  </div>

  <div id="forecast" class="forecast"></div>

</div>

<div class="card">

  <div class="section-title">
    📍 Τοποθεσία
  </div>

  <div id="map"></div>

</div>

</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

/* =========================================
   ΤΡΕΧΟΥΣΑ ΤΟΠΟΘΕΣΙΑ
========================================= */

let currentLat = 40.6401;
let currentLon = 22.9444;

let map;
let marker;


/* =========================================
   WEATHER CODES
========================================= */

function weatherInfo(code){

  const w = {

    0:["☀️","Αίθριος"],
    1:["🌤️","Κυρίως αίθριος"],
    2:["⛅","Λίγες νεφώσεις"],
    3:["☁️","Συννεφιά"],

    45:["🌫️","Ομίχλη"],
    48:["🌫️","Ομίχλη με πάχνη"],

    51:["🌦️","Ασθενής ψιχάλα"],
    53:["🌦️","Ψιχάλα"],
    55:["🌧️","Ισχυρή ψιχάλα"],

    56:["🌧️❄️","Παγωμένη ψιχάλα"],
    57:["🌧️❄️","Ισχυρή παγωμένη ψιχάλα"],

    61:["🌧️","Ασθενής βροχή"],
    63:["🌧️","Βροχή"],
    65:["🌧️","Ισχυρή βροχή"],

    66:["🌧️❄️","Παγωμένη βροχή"],
    67:["🌧️❄️","Ισχυρή παγωμένη βροχή"],

    71:["🌨️","Ασθενής χιονόπτωση"],
    73:["❄️","Χιονόπτωση"],
    75:["❄️","Ισχυρή χιονόπτωση"],
    77:["❄️","Χιονόκοκκοι"],

    80:["🌦️","Ασθενείς μπόρες"],
    81:["🌧️","Μπόρες"],
    82:["⛈️","Ισχυρές μπόρες"],

    85:["🌨️","Ασθενείς χιονομπόρες"],
    86:["❄️","Ισχυρές χιονομπόρες"],

    95:["⛈️","Καταιγίδα"],
    96:["⛈️","Καταιγίδα με χαλάζι"],
    99:["⛈️","Ισχυρή καταιγίδα με χαλάζι"]
  };

  return w[code] || ["🌡️","Μεταβλητός καιρός"];
}


/* =========================================
   ΛΗΨΗ ECMWF IFS HRES
========================================= */

async function getIFS(){

  const url =
    "https://api.open-meteo.com/v1/forecast" +
    "?latitude=" + currentLat +
    "&longitude=" + currentLon +
    "&models=ecmwf_ifs025" +
    "&daily=" +
    "temperature_2m_max," +
    "temperature_2m_min," +
    "precipitation_sum," +
    "rain_sum," +
    "snowfall_sum," +
    "weather_code" +
    "&current=" +
    "temperature_2m,weather_code" +
    "&forecast_days=15" +
    "&timezone=auto" +
    "&temperature_unit=celsius" +
    "&precipitation_unit=mm";

  const r = await fetch(url,{cache:"no-store"});

  if(!r.ok) throw new Error("IFS error");

  return await r.json();
}


/* =========================================
   ΛΗΨΗ ECMWF AIFS
========================================= */

async function getAIFS(){

  const url =
    "https://api.open-meteo.com/v1/forecast" +
    "?latitude=" + currentLat +
    "&longitude=" + currentLon +
    "&models=ecmwf_aifs025" +
    "&daily=" +
    "temperature_2m_max," +
    "temperature_2m_min," +
    "precipitation_sum," +
    "rain_sum," +
    "snowfall_sum," +
    "weather_code" +
    "&current=" +
    "temperature_2m,weather_code" +
    "&forecast_days=15" +
    "&timezone=auto" +
    "&temperature_unit=celsius" +
    "&precipitation_unit=mm";

  const r = await fetch(url,{cache:"no-store"});

  if(!r.ok) throw new Error("AIFS error");

  return await r.json();
}


/* =========================================
   ΜΕΣΟΣ ΟΡΟΣ
========================================= */

function avg(a,b){

  if(a == null && b == null) return 0;
  if(a == null) return b;
  if(b == null) return a;

  return (a+b)/2;
}


/* =========================================
   ΚΑΤΑΣΤΑΣΗ ΚΑΙΡΟΥ
========================================= */

function chooseWeatherCode(
  codeIFS,
  codeAIFS,
  snowIFS,
  snowAIFS,
  rainIFS,
  rainAIFS
){

  /*
    Δεν κάνουμε ΠΟΤΕ:
    Math.max(codeIFS,codeAIFS)

    Οι WMO κωδικοί είναι κατηγορίες.
  */

  const snow =
    avg(snowIFS,snowAIFS);

  const rain =
    avg(rainIFS,rainAIFS);


  const snowCodes =
    [71,73,75,77,85,86];

  const stormCodes =
    [95,96,99];

  const rainCodes =
    [51,53,55,61,63,65,66,67,80,81,82];

  const fogCodes =
    [45,48];


  /*
    Αν υπάρχει πραγματικό snowfall
    από τα μοντέλα, προτεραιότητα στο χιόνι.
  */

  if(snow > 0){

    if(snowIFS > 0 && snowAIFS > 0){

      return snowCodes.includes(codeIFS)
        ? codeIFS
        : codeAIFS;
    }

    if(snowIFS > 0){

      return snowCodes.includes(codeIFS)
        ? codeIFS
        : 71;
    }

    if(snowAIFS > 0){

      return snowCodes.includes(codeAIFS)
        ? codeAIFS
        : 71;
    }
  }


  /*
    Καταιγίδα:
    αν και τα δύο μοντέλα τη δείχνουν,
    κρατάμε την πραγματική κατηγορία.
  */

  if(
    stormCodes.includes(codeIFS) &&
    stormCodes.includes(codeAIFS)
  ){

    return codeIFS;
  }


  /*
    Αν συμφωνούν τα δύο μοντέλα,
    χρησιμοποιούμε αυτόν τον κωδικό.
  */

  if(codeIFS === codeAIFS){

    return codeIFS;
  }


  /*
    Αν διαφωνούν αλλά υπάρχει βροχή,
    δεν επιλέγουμε αυθαίρετα με βάση
    το μεγαλύτερο νούμερο.
  */

  if(rain > 0){

    if(rainCodes.includes(codeIFS))
      return codeIFS;

    if(rainCodes.includes(codeAIFS))
      return codeAIFS;
  }


  /*
    Ομίχλη
  */

  if(fogCodes.includes(codeIFS))
    return codeIFS;

  if(fogCodes.includes(codeAIFS))
    return codeAIFS;


  /*
    Τελική επιλογή IFS.
  */

  return codeIFS;
}


/* =========================================
   ΦΟΡΤΩΣΗ
========================================= */

async function loadWeather(){

  document.getElementById("status").textContent =
    "Φόρτωση πραγματικών δεδομένων ECMWF...";

  try{

    const [ifs,aifs] =
      await Promise.all([
        getIFS(),
        getAIFS()
      ]);

    renderCurrent(ifs,aifs);
    renderForecast(ifs,aifs);

    document.getElementById("status").textContent = "";

  }catch(error){

    console.error(error);

    document.getElementById("status").textContent =
      "Σφάλμα φόρτωσης δεδομένων. Δοκιμάζεται ξανά...";

    setTimeout(loadWeather,5000);
  }
}


/* =========================================
   ΤΡΕΧΩΝ ΚΑΙΡΟΣ
========================================= */

function renderCurrent(ifs,aifs){

  const temp =
    avg(
      ifs.current.temperature_2m,
      aifs.current.temperature_2m
    );


  const code =
    chooseWeatherCode(
      ifs.current.weather_code,
      aifs.current.weather_code,
      0,
      0,
      0,
      0
    );


  const info =
    weatherInfo(code);


  document.getElementById("currentTemp")
    .textContent =
    Math.round(temp) + "°";


  document.getElementById("currentIcon")
    .textContent =
    info[0];


  document.getElementById("currentCondition")
    .textContent =
    info[1];
}


/* =========================================
   15 ΗΜΕΡΕΣ
========================================= */

function renderForecast(ifs,aifs){

  const box =
    document.getElementById("forecast");

  box.innerHTML="";


  for(let i=0;i<15;i++){

    /*
      ΠΡΑΓΜΑΤΙΚΟΣ ΜΕΣΟΣ ΟΡΟΣ
    */

    const max =
      avg(
        ifs.daily.temperature_2m_max[i],
        aifs.daily.temperature_2m_max[i]
      );

    const min =
      avg(
        ifs.daily.temperature_2m_min[i],
        aifs.daily.temperature_2m_min[i]
      );

    const precipitation =
      avg(
        ifs.daily.precipitation_sum[i],
        aifs.daily.precipitation_sum[i]
      );

    const rain =
      avg(
        ifs.daily.rain_sum[i],
        aifs.daily.rain_sum[i]
      );

    const snow =
      avg(
        ifs.daily.snowfall_sum[i],
        aifs.daily.snowfall_sum[i]
      );


    const code =
      chooseWeatherCode(
        ifs.daily.weather_code[i],
        aifs.daily.weather_code[i],

        ifs.daily.snowfall_sum[i],
        aifs.daily.snowfall_sum[i],

        ifs.daily.rain_sum[i],
        aifs.daily.rain_sum[i]
      );


    const info =
      weatherInfo(code);


    const date =
      new Date(
        ifs.daily.time[i] + "T12:00:00"
      );


    const day =
      date.toLocaleDateString(
        "el-GR",
        {weekday:"short"}
      );

    const dateText =
      date.toLocaleDateString(
        "el-GR",
        {
          day:"numeric",
          month:"short"
        }
      );


    const card =
      document.createElement("div");

    card.className="day";


    let precipText;

    if(snow > 0){

      precipText =
        "❄️ " +
        snow.toFixed(1) +
        " cm";

    }else if(rain > 0){

      precipText =
        "🌧️ " +
        rain.toFixed(1) +
        " mm";

    }else if(precipitation > 0){

      precipText =
        "💧 " +
        precipitation.toFixed(1) +
        " mm";

    }else{

      precipText =
        "☔ 0 mm";
    }


    card.innerHTML = `

      <div class="day-name">
        ${day}<br>
        <small>${dateText}</small>
      </div>

      <div class="day-icon">
        ${info[0]}
      </div>

      <div class="high">
        ${Math.round(max)}°
      </div>

      <div class="low">
        ${Math.round(min)}°
      </div>

      <div class="precip">
        ${precipText}
      </div>

    `;


    box.appendChild(card);
  }
}


/* =========================================
   ΑΝΑΖΗΤΗΣΗ ΠΑΓΚΟΣΜΙΩΣ
========================================= */

async function searchLocation(){

  const input =
    document.getElementById("searchInput");

  const query =
    input.value.trim();

  if(!query) return;


  document.getElementById("status")
    .textContent =
    "Αναζήτηση περιοχής...";


  try{

    const url =
      "https://geocoding-api.open-meteo.com/v1/search" +
      "?name=" +
      encodeURIComponent(query) +
      "&count=1" +
      "&language=el" +
      "&format=json";


    const response =
      await fetch(url,{cache:"no-store"});


    const data =
      await response.json();


    if(
      !data.results ||
      !data.results.length
    ){

      document.getElementById("status")
        .textContent =
        "Δεν βρέθηκε η περιοχή.";

      return;
    }


    const place =
      data.results[0];


    selectCity(
      place.name +
      (
        place.country
          ? ", " + place.country
          : ""
      ),
      place.latitude,
      place.longitude
    );


  }catch(error){

    console.error(error);

    document.getElementById("status")
      .textContent =
      "Σφάλμα στην αναζήτηση.";
  }
}


/* =========================================
   ΕΠΙΛΟΓΗ ΠΟΛΗΣ
========================================= */

function selectCity(name,lat,lon){

  currentLat = lat;
  currentLon = lon;

  document.getElementById("locationName")
    .textContent =
    name;

  updateMap(lat,lon,name);

  loadWeather();
}


/* =========================================
   MAP
========================================= */

function initMap(){

  map =
    L.map("map");


  L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
      attribution:
        "&copy; OpenStreetMap contributors"
    }
  ).addTo(map);


  updateMap(
    currentLat,
    currentLon,
    "Θεσσαλονίκη"
  );
}


function updateMap(lat,lon,name){

  if(!map) return;


  map.setView(
    [lat,lon],
    10
  );


  if(marker){

    map.removeLayer(marker);
  }


  marker =
    L.marker([lat,lon])
      .addTo(map)
      .bindPopup(
        "<b>" + name + "</b>"
      )
      .openPopup();
}


/* =========================================
   ENTER = SEARCH
========================================= */

document
  .getElementById("searchInput")
  .addEventListener(
    "keydown",
    function(e){

      if(e.key === "Enter"){
        searchLocation();
      }

    }
  );


/* =========================================
   START
========================================= */

initMap();

loadWeather();

</script>

</body>
</html>
