<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

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
  font-family:Arial, sans-serif;
  background:linear-gradient(135deg,#07111f,#102b4d,#163e68);
  color:white;
  min-height:100vh;
}

.container{
  width:94%;
  max-width:1200px;
  margin:auto;
  padding:25px 0 50px;
}

header{
  text-align:center;
  margin-bottom:25px;
}

header h1{
  font-size:36px;
  margin-bottom:7px;
}

header p{
  color:#bcd0e8;
}

.search{
  display:flex;
  gap:10px;
  max-width:750px;
  margin:20px auto;
}

.search input{
  flex:1;
  padding:15px;
  border:0;
  border-radius:14px;
  font-size:16px;
  outline:none;
}

.search button{
  border:0;
  border-radius:14px;
  padding:0 22px;
  background:#2d8cff;
  color:white;
  font-size:16px;
  cursor:pointer;
}

.city-buttons{
  display:flex;
  flex-wrap:wrap;
  justify-content:center;
  gap:9px;
  margin-bottom:25px;
}

.city-buttons button{
  background:rgba(255,255,255,.10);
  color:white;
  border:1px solid rgba(255,255,255,.15);
  border-radius:12px;
  padding:10px 14px;
  cursor:pointer;
}

.card{
  background:rgba(255,255,255,.09);
  border:1px solid rgba(255,255,255,.12);
  backdrop-filter:blur(12px);
  border-radius:22px;
  padding:22px;
  margin-bottom:20px;
  box-shadow:0 12px 35px rgba(0,0,0,.18);
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
  font-size:64px;
}

.current-temp{
  font-size:55px;
  font-weight:bold;
}

.condition{
  font-size:19px;
  color:#d5e5f5;
  margin-top:5px;
}

.section-title{
  font-size:24px;
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
  padding:16px 10px;
  text-align:center;
  min-height:190px;
}

.day-name{
  font-weight:bold;
  margin-bottom:9px;
}

.day-icon{
  font-size:42px;
  margin:8px 0;
}

.high{
  font-size:21px;
  font-weight:bold;
}

.low{
  font-size:16px;
  color:#bcd0e8;
  margin-top:4px;
}

.rain{
  font-size:13px;
  color:#9fcaff;
  margin-top:9px;
}

#map{
  height:380px;
  width:100%;
  border-radius:18px;
  overflow:hidden;
}

.status{
  text-align:center;
  color:#bcd0e8;
  margin:10px 0;
}

.error{
  color:#ff9f9f;
  text-align:center;
  margin:15px;
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
    font-size:45px;
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
  <p>Πρόγνωση καιρού με δεδομένα ECMWF</p>
</header>

<div class="search">
  <input id="searchInput"
         placeholder="Αναζήτησε πόλη ή περιοχή σε όλο τον κόσμο">
  <button onclick="searchLocation()">Αναζήτηση</button>
</div>

<div class="city-buttons">
  <button onclick="selectCity('Αθήνα',37.9838,23.7275)">Αθήνα</button>
  <button onclick="selectCity('Θεσσαλονίκη',40.6401,22.9444)">Θεσσαλονίκη</button>
  <button onclick="selectCity('Πάτρα',38.2466,21.7346)">Πάτρα</button>
  <button onclick="selectCity('Λάρισα',39.6390,22.4191)">Λάρισα</button>
  <button onclick="selectCity('Ηράκλειο',35.3387,25.1442)">Ηράκλειο</button>
  <button onclick="selectCity('Ιωάννινα',39.6650,20.8537)">Ιωάννινα</button>
  <button onclick="selectCity('Καβάλα',40.9396,24.4018)">Καβάλα</button>
  <button onclick="selectCity('Ρόδος',36.4349,28.2176)">Ρόδος</button>
</div>

<div id="status" class="status"></div>

<div class="card current">

  <div id="locationName" class="location">Θεσσαλονίκη</div>

  <div class="current-weather">

    <div id="currentIcon" class="current-icon">🌤️</div>

    <div>
      <div id="currentTemp" class="current-temp">--°</div>
      <div id="currentCondition" class="condition">Φόρτωση...</div>
    </div>

  </div>

</div>

<div class="card">

  <div class="section-title">📅 Πρόγνωση 15 ημερών</div>

  <div id="forecast" class="forecast"></div>

</div>

<div class="card">

  <div class="section-title">📍 Τοποθεσία</div>

  <div id="map"></div>

</div>

</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

let currentLat = 40.6401;
let currentLon = 22.9444;

let map;
let marker;


/* -----------------------------
   WMO WEATHER CODES
----------------------------- */

function weatherInfo(code){

  const data = {

    0:["☀️","Αίθριος"],
    1:["🌤️","Κυρίως αίθριος"],
    2:["⛅","Λίγες νεφώσεις"],
    3:["☁️","Συννεφιά"],

    45:["🌫️","Ομίχλη"],
    48:["🌫️","Ομίχλη με πάχνη"],

    51:["🌦️","Ασθενής ψιχάλα"],
    53:["🌦️","Ψιχάλα"],
    55:["🌧️","Ισχυρή ψιχάλα"],

    56:["🌧️","Ασθενής παγωμένη ψιχάλα"],
    57:["🌧️","Ισχυρή παγωμένη ψιχάλα"],

    61:["🌧️","Ασθενής βροχή"],
    63:["🌧️","Βροχή"],
    65:["🌧️","Ισχυρή βροχή"],

    66:["🌧️❄️","Ασθενής παγωμένη βροχή"],
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

  return data[code] || ["🌡️","Μεταβλητός καιρός"];
}


/* -----------------------------
   MODEL FORECAST
   IFS 0.25° + AIFS 0.25°
----------------------------- */

async function getModelForecast(model){

  const url =
    "https://api.open-meteo.com/v1/forecast" +
    "?latitude=" + currentLat +
    "&longitude=" + currentLon +
    "&models=" + model +
    "&daily=" +
    "temperature_2m_max," +
    "temperature_2m_min," +
    "precipitation_sum," +
    "rain_sum," +
    "snowfall_sum," +
    "weather_code" +
    "&current=temperature_2m,weather_code" +
    "&forecast_days=15" +
    "&timezone=auto" +
    "&temperature_unit=celsius" +
    "&precipitation_unit=mm";

  const response = await fetch(url,{cache:"no-store"});

  if(!response.ok){
    throw new Error("API error");
  }

  return await response.json();
}


/* -----------------------------
   AVERAGE OF IFS + AIFS
----------------------------- */

async function loadWeather(){

  document.getElementById("status").textContent =
    "Φόρτωση πραγματικών δεδομένων ECMWF...";

  try{

    const [ifs,aifs] = await Promise.all([

      getModelForecast("ecmwf_ifs025"),
      getModelForecast("ecmwf_aifs025")

    ]);

    renderCurrent(ifs,aifs);
    renderForecast(ifs,aifs);

    document.getElementById("status").textContent = "";

  }catch(error){

    console.error(error);

    document.getElementById("status").textContent =
      "Δεν ήταν δυνατή η φόρτωση των δεδομένων.";

  }

}


/* -----------------------------
   CURRENT WEATHER
----------------------------- */

function renderCurrent(ifs,aifs){

  const tempIFS = ifs.current.temperature_2m;
  const tempAIFS = aifs.current.temperature_2m;

  const averageTemp =
    (tempIFS + tempAIFS) / 2;

  const codeIFS = ifs.current.weather_code;
  const codeAIFS = aifs.current.weather_code;

  /*
    Για την τρέχουσα κατάσταση:
    αν ένα από τα δύο μοντέλα δείχνει χιόνι
    και υπάρχει πραγματική χιονόπτωση,
    δεν το μετατρέπουμε σε βροχή.
  */

  const snowCodes =
    [71,73,75,77,85,86];

  let finalCode;

  if(
    snowCodes.includes(codeIFS) &&
    snowCodes.includes(codeAIFS)
  ){

    finalCode = codeIFS;

  }else if(snowCodes.includes(codeIFS)){

    finalCode = codeIFS;

  }else if(snowCodes.includes(codeAIFS)){

    finalCode = codeAIFS;

  }else{

    /*
      Όταν δεν υπάρχει χιόνι,
      παίρνουμε τον κωδικό του IFS,
      χωρίς Math.max σε WMO codes.
    */

    finalCode = codeIFS;

  }

  const info = weatherInfo(finalCode);

  document.getElementById("currentTemp").textContent =
    Math.round(averageTemp) + "°";

  document.getElementById("currentIcon").textContent =
    info[0];

  document.getElementById("currentCondition").textContent =
    info[1];
}


/* -----------------------------
   15 DAY FORECAST
----------------------------- */

function renderForecast(ifs,aifs){

  const container =
    document.getElementById("forecast");

  container.innerHTML="";

  const days = ifs.daily.time;

  for(let i=0;i<15;i++){

    /*
      ΙΔΙΟΣ ΜΕΣΟΣ ΟΡΟΣ:
      IFS + AIFS / 2
    */

    const max =
      (
        ifs.daily.temperature_2m_max[i] +
        aifs.daily.temperature_2m_max[i]
      ) / 2;

    const min =
      (
        ifs.daily.temperature_2m_min[i] +
        aifs.daily.temperature_2m_min[i]
      ) / 2;

    const rain =
      (
        ifs.daily.rain_sum[i] +
        aifs.daily.rain_sum[i]
      ) / 2;

    const snow =
      (
        ifs.daily.snowfall_sum[i] +
        aifs.daily.snowfall_sum[i]
      ) / 2;

    const codeIFS =
      ifs.daily.weather_code[i];

    const codeAIFS =
      aifs.daily.weather_code[i];


    /*
      ΧΙΟΝΙ:
      Δεν χρησιμοποιούμε τη θερμοκρασία
      για να "μαντέψουμε" χιόνι.

      Χρησιμοποιούμε το πραγματικό
      snowfall_sum των μοντέλων.
    */

    let finalCode;

    const snowCodes =
      [71,73,75,77,85,86];

    const ifsSnow =
      snowCodes.includes(codeIFS);

    const aifsSnow =
      snowCodes.includes(codeAIFS);


    /*
      Αν υπάρχει πραγματικό snowfall
      σε κάποιο από τα δύο μοντέλα,
      το εμφανίζουμε σωστά.
    */

    if(snow > 0){

      if(ifsSnow || aifsSnow){

        finalCode =
          ifsSnow ? codeIFS : codeAIFS;

      }else{

        /*
          Αν υπάρχει snowfall αλλά ο ημερήσιος
          κωδικός είναι μικτός/διαφορετικός,
          χρησιμοποιούμε χιονόπτωση.
        */

        finalCode = 71;
      }

    }else{

      /*
        Χωρίς χιόνι δεν συγκρίνουμε αριθμητικά
        WMO codes.
      */

      finalCode = codeIFS;
    }


    const info =
      weatherInfo(finalCode);


    const date =
      new Date(days[i]);

    const dayName =
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

    card.innerHTML=`

      <div class="day-name">
        ${dayName}<br>
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

      <div class="rain">
        ${snow > 0
          ? "❄️ " + snow.toFixed(1) + " cm"
          : "🌧️ " + rain.toFixed(1) + " mm"
        }
      </div>

    `;

    container.appendChild(card);
  }
}


/* -----------------------------
   SEARCH WORLDWIDE
----------------------------- */

async function searchLocation(){

  const input =
    document.getElementById("searchInput");

  const query =
    input.value.trim();

  if(!query) return;

  document.getElementById("status").textContent =
    "Αναζήτηση...";

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

    if(!data.results || !data.results.length){

      document.getElementById("status").textContent =
        "Δεν βρέθηκε η περιοχή.";

      return;
    }

    const place =
      data.results[0];

    selectCity(
      place.name +
      (place.country ? ", " + place.country : ""),
      place.latitude,
      place.longitude
    );

  }catch(error){

    console.error(error);

    document.getElementById("status").textContent =
      "Σφάλμα στην αναζήτηση.";

  }
}


/* -----------------------------
   SELECT LOCATION
----------------------------- */

function selectCity(name,lat,lon){

  currentLat = lat;
  currentLon = lon;

  document.getElementById("locationName").textContent =
    name;

  updateMap(
    lat,
    lon,
    name
  );

  loadWeather();
}


/* -----------------------------
   MAP
----------------------------- */

function initMap(){

  map =
    L.map("map");

  L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
      attribution:
      '&copy; OpenStreetMap contributors'
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
      "<b>" +
      name +
      "</b>"
    )
    .openPopup();
}


/* -----------------------------
   ENTER KEY SEARCH
----------------------------- */

document
  .getElementById("searchInput")
  .addEventListener(
    "keydown",
    function(event){

      if(event.key === "Enter"){
        searchLocation();
      }

    }
  );


/* START */

initMap();

loadWeather();

</script>

</body>
</html>
