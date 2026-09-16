<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>WORLD WEATHER</title>

<link rel="stylesheet"
      href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

<style>
*{
  box-sizing:border-box;
}

html,body{
  margin:0;
  padding:0;
  min-height:100%;
}

body{
  font-family:Arial,Helvetica,sans-serif;
  color:#fff;
  background:
    radial-gradient(circle at top left,#174d82 0%,transparent 35%),
    linear-gradient(135deg,#06152b,#0b2949 55%,#071526);
}

.container{
  width:min(1200px,94%);
  margin:auto;
  padding:25px 0 45px;
}

header{
  text-align:center;
  margin-bottom:25px;
}

header h1{
  margin:0;
  font-size:clamp(30px,6vw,55px);
  letter-spacing:-1px;
}

header p{
  margin:8px 0 0;
  color:#bcd5ec;
  font-size:15px;
}

.glass{
  background:rgba(255,255,255,.09);
  border:1px solid rgba(255,255,255,.13);
  box-shadow:0 15px 45px rgba(0,0,0,.25);
  backdrop-filter:blur(14px);
  -webkit-backdrop-filter:blur(14px);
  border-radius:22px;
}

.search-box{
  padding:18px;
  display:flex;
  gap:10px;
  margin-bottom:12px;
}

.search-box input{
  flex:1;
  min-width:0;
  padding:15px 17px;
  border-radius:14px;
  border:none;
  outline:none;
  background:#fff;
  color:#10233d;
  font-size:16px;
}

.search-box button{
  border:none;
  border-radius:14px;
  padding:0 22px;
  background:#2788d9;
  color:#fff;
  font-size:16px;
  font-weight:bold;
  cursor:pointer;
}

.search-box button:disabled{
  opacity:.55;
  cursor:wait;
}

.results{
  display:none;
  flex-wrap:wrap;
  gap:8px;
  margin-bottom:15px;
}

.result-btn{
  border:1px solid rgba(255,255,255,.15);
  background:rgba(255,255,255,.09);
  color:#fff;
  padding:10px 14px;
  border-radius:14px;
  cursor:pointer;
  text-align:left;
}

.result-btn:hover{
  background:rgba(255,255,255,.17);
}

.cities{
  display:flex;
  gap:8px;
  flex-wrap:wrap;
  margin-bottom:18px;
}

.city-btn{
  border:1px solid rgba(255,255,255,.15);
  background:rgba(255,255,255,.08);
  color:#fff;
  padding:9px 14px;
  border-radius:999px;
  cursor:pointer;
}

.city-btn:hover{
  background:rgba(255,255,255,.15);
}

.status{
  min-height:24px;
  margin:5px 3px 15px;
  color:#bcd5ec;
  font-size:14px;
}

.current{
  padding:25px;
  margin-bottom:20px;
}

.location-name{
  font-size:28px;
  font-weight:bold;
  margin-bottom:20px;
}

.current-temp{
  font-size:clamp(55px,11vw,90px);
  font-weight:700;
  line-height:1;
  margin-bottom:20px;
}

.current-details{
  display:flex;
  gap:18px;
  flex-wrap:wrap;
  color:#dcecff;
  font-size:16px;
}

.current-details span{
  background:rgba(255,255,255,.07);
  padding:9px 12px;
  border-radius:12px;
}

.section-title{
  margin:25px 0 13px;
  font-size:22px;
}

.forecast{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(135px,1fr));
  gap:10px;
}

.day{
  padding:16px 12px;
  text-align:center;
  min-height:225px;
}

.day-date{
  font-size:14px;
  color:#bdd5ec;
  margin-bottom:12px;
}

.day-icon{
  font-size:38px;
  margin:7px 0;
}

.day-condition{
  min-height:35px;
  font-size:13px;
  color:#dcecff;
  line-height:1.25;
}

.temps{
  margin-top:13px;
  display:flex;
  flex-direction:column;
  align-items:center;
  gap:2px;
}

.temp-high{
  font-size:20px;
  font-weight:bold;
}

.temp-low{
  font-size:17px;
  color:#b9d1e8;
}

.rain{
  margin-top:9px;
  color:#9dd7ff;
  font-size:13px;
}

.snow{
  margin-top:4px;
  color:#e3f4ff;
  font-size:13px;
}

.map-card{
  padding:14px;
  margin-top:20px;
}

#map{
  width:100%;
  height:400px;
  border-radius:16px;
  overflow:hidden;
}

.footer{
  text-align:center;
  color:#8eabc5;
  font-size:12px;
  margin-top:25px;
}

@media(max-width:600px){

  .search-box{
    flex-direction:column;
  }

  .search-box button{
    padding:14px;
  }

  .forecast{
    grid-template-columns:repeat(2,1fr);
  }

  #map{
    height:320px;
  }
}
</style>
</head>

<body>

<div class="container">

<header>
  <h1>🌍 WORLD WEATHER</h1>
  <p>Global weather forecast</p>
</header>

<div class="search-box glass">

  <input
    id="searchInput"
    type="text"
    placeholder="Αναζήτησε οποιαδήποτε υπαρκτή περιοχή στον κόσμο..."
    autocomplete="off"
  >

  <button id="searchButton">
    Αναζήτηση
  </button>

</div>

<div id="results" class="results"></div>

<div class="cities">

  <button class="city-btn"
    onclick="loadLocation('Αθήνα',37.9838,23.7275)">
    Αθήνα
  </button>

  <button class="city-btn"
    onclick="loadLocation('Θεσσαλονίκη',40.6401,22.9444)">
    Θεσσαλονίκη
  </button>

  <button class="city-btn"
    onclick="loadLocation('Λονδίνο',51.5074,-0.1278)">
    Λονδίνο
  </button>

  <button class="city-btn"
    onclick="loadLocation('Νέα Υόρκη',40.7128,-74.0060)">
    Νέα Υόρκη
  </button>

  <button class="city-btn"
    onclick="loadLocation('Τόκιο',35.6762,139.6503)">
    Τόκιο
  </button>

  <button class="city-btn"
    onclick="loadLocation('Ντουμπάι',25.2048,55.2708)">
    Ντουμπάι
  </button>

  <button class="city-btn"
    onclick="loadLocation('Ρέικιαβικ',64.1466,-21.9426)">
    Ρέικιαβικ
  </button>

</div>

<div id="status" class="status"></div>

<section class="current glass">

  <div id="locationName" class="location-name">
    Θεσσαλονίκη
  </div>

  <div id="currentTemp" class="current-temp">
    --°
  </div>

  <div class="current-details">

    <span id="humidity">
      💧 --%
    </span>

    <span id="windSpeed">
      💨 -- km/h
    </span>

    <span id="windDirection">
      🧭 --
    </span>

  </div>

</section>

<h2 class="section-title">
  15ήμερη πρόγνωση
</h2>

<section id="forecast" class="forecast"></section>

<h2 class="section-title">
  Χάρτης περιοχής
</h2>

<section class="map-card glass">
  <div id="map"></div>
</section>

<div class="footer">
  Weather data from ECMWF via Open-Meteo
</div>

</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

/* =========================================================
   GLOBAL STATE
========================================================= */

let map = null;
let marker = null;

let controller = null;
let requestId = 0;

let selectedLat = 40.6401;
let selectedLon = 22.9444;
let selectedName = "Θεσσαλονίκη";


/* =========================================================
   WMO WEATHER CODES
========================================================= */

const WMO = {

  0:["☀️","Καθαρός ουρανός"],

  1:["🌤️","Κυρίως αίθριος"],
  2:["⛅","Μερική συννεφιά"],
  3:["☁️","Συννεφιά"],

  45:["🌫️","Ομίχλη"],
  48:["🌫️","Ομίχλη με πάχνη"],

  51:["🌦️","Ασθενές ψιλόβροχο"],
  53:["🌦️","Μέτριο ψιλόβροχο"],
  55:["🌧️","Ισχυρό ψιλόβροχο"],

  56:["🌧️❄️","Παγωμένο ψιλόβροχο"],
  57:["🌧️❄️","Ισχυρό παγωμένο ψιλόβροχο"],

  61:["🌧️","Ασθενής βροχή"],
  63:["🌧️","Μέτρια βροχή"],
  65:["🌧️","Ισχυρή βροχή"],

  66:["🌧️❄️","Παγωμένη βροχή"],
  67:["🌧️❄️","Ισχυρή παγωμένη βροχή"],

  71:["🌨️","Ασθενής χιονόπτωση"],
  73:["❄️","Μέτρια χιονόπτωση"],
  75:["❄️","Ισχυρή χιονόπτωση"],

  77:["❄️","Κόκκοι χιονιού"],

  80:["🌦️","Ασθενείς μπόρες"],
  81:["🌧️","Μέτριες μπόρες"],
  82:["⛈️","Ισχυρές μπόρες"],

  85:["🌨️","Ασθενείς χιονομπόρες"],
  86:["🌨️","Ισχυρές χιονομπόρες"],

  95:["⛈️","Καταιγίδα"],
  96:["⛈️","Καταιγίδα με χαλάζι"],
  99:["⛈️","Ισχυρή καταιγίδα με χαλάζι"]
};


function getWeather(code){

  return WMO[code] || ["🌡️","Μεταβλητός καιρός"];

}


/* =========================================================
   NUMBER AVERAGE
========================================================= */

function average(a,b){

  if(a == null && b == null) return null;
  if(a == null) return b;
  if(b == null) return a;

  return (Number(a) + Number(b)) / 2;

}


/* =========================================================
   CIRCULAR WIND AVERAGE
========================================================= */

function averageWindDirection(a,b){

  if(a == null && b == null) return null;
  if(a == null) return b;
  if(b == null) return a;

  const aRad = Number(a) * Math.PI / 180;
  const bRad = Number(b) * Math.PI / 180;

  const x =
    Math.cos(aRad) +
    Math.cos(bRad);

  const y =
    Math.sin(aRad) +
    Math.sin(bRad);

  let degrees =
    Math.atan2(y,x) * 180 / Math.PI;

  if(degrees < 0)
    degrees += 360;

  return degrees;
}


function windDirection(degrees){

  if(degrees == null)
    return "--";

  const directions = [
    "Β",
    "ΒΒΑ",
    "ΒΑ",
    "ΑΒΑ",
    "Α",
    "ΑΝΑ",
    "ΝΑ",
    "ΝΝΑ",
    "Ν",
    "ΝΝΔ",
    "ΝΔ",
    "ΔΝΔ",
    "Δ",
    "ΔΒΔ",
    "ΒΔ",
    "ΒΒΔ"
  ];

  return directions[
    Math.round(degrees / 22.5) % 16
  ];
}


/* =========================================================
   MODEL REQUEST
========================================================= */

function modelURL(model,lat,lon){

  /*
    Both models are requested from Open-Meteo.
    IFS HRES = ECMWF native 9 km.
    AIFS = ECMWF AI model.
  */

  const base =
    "https://api.open-meteo.com/v1/forecast";

  const params = new URLSearchParams({

    latitude:lat,
    longitude:lon,

    models:model,

    current:
      "temperature_2m," +
      "relative_humidity_2m," +
      "wind_speed_10m," +
      "wind_direction_10m," +
      "weather_code," +
      "precipitation," +
      "rain," +
      "snowfall",

    daily:
      "temperature_2m_max," +
      "temperature_2m_min," +
      "precipitation_sum," +
      "rain_sum," +
      "snowfall_sum," +
      "weather_code",

    forecast_days:"15",
    timezone:"auto",

    temperature_unit:"celsius",
    wind_speed_unit:"kmh",
    precipitation_unit:"mm"
  });

  return base + "?" + params.toString();
}


async function getModel(
  model,
  lat,
  lon,
  signal
){

  const response =
    await fetch(
      modelURL(model,lat,lon),
      {
        signal,
        cache:"no-store"
      }
    );

  if(!response.ok)
    throw new Error(
      "Weather request failed: " +
      response.status
    );

  const data =
    await response.json();

  if(
    data.error ||
    !data.current ||
    !data.daily
  ){
    throw new Error(
      "Invalid weather data"
    );
  }

  return data;
}


/* =========================================================
   LOAD BOTH MODELS
========================================================= */

async function loadModels(
  lat,
  lon,
  signal
){

  /*
    They run simultaneously.
    Promise.all means we only use the
    result when BOTH real model responses
    have arrived.
  */

  const results =
    await Promise.all([

      getModel(
        "ecmwf_ifs025",
        lat,
        lon,
        signal
      ),

      getModel(
        "ecmwf_aifs025",
        lat,
        lon,
        signal
      )

    ]);

  return {
    ifs:results[0],
    aifs:results[1]
  };
}


/* =========================================================
   CURRENT CONDITIONS
========================================================= */

function renderCurrent(
  ifs,
  aifs
){

  /*
    These are actual current model values.
    We average IFS + AIFS numerically.
  */

  const temperature =
    average(
      ifs.current.temperature_2m,
      aifs.current.temperature_2m
    );

  const humidity =
    average(
      ifs.current.relative_humidity_2m,
      aifs.current.relative_humidity_2m
    );

  const wind =
    average(
      ifs.current.wind_speed_10m,
      aifs.current.wind_speed_10m
    );

  const direction =
    averageWindDirection(
      ifs.current.wind_direction_10m,
      aifs.current.wind_direction_10m
    );

  document.getElementById(
    "currentTemp"
  ).textContent =
    Math.round(temperature) + "°";

  document.getElementById(
    "humidity"
  ).textContent =
    "💧 " +
    Math.round(humidity) +
    "%";

  document.getElementById(
    "windSpeed"
  ).textContent =
    "💨 " +
    Math.round(wind) +
    " km/h";

  document.getElementById(
    "windDirection"
  ).textContent =
    "🧭 " +
    windDirection(direction);
}


/* =========================================================
   WEATHER TYPE
========================================================= */

function conditionFromModels(
  code1,
  code2,
  rain,
  snow
){

  /*
    Precipitation quantities have priority.
    This prevents a cold place with snowfall
    from incorrectly displaying plain rain.
  */

  if(Number(snow) > 0.05){

    const snowCodes =
      [71,73,75,77,85,86];

    if(snowCodes.includes(code1))
      return getWeather(code1);

    if(snowCodes.includes(code2))
      return getWeather(code2);

    return ["❄️","Χιονόπτωση"];
  }

  if(Number(rain) > 0.05){

    const rainCodes =
      [
        51,53,55,
        56,57,
        61,63,65,
        66,67,
        80,81,82,
        95,96,99
      ];

    if(rainCodes.includes(code1))
      return getWeather(code1);

    if(rainCodes.includes(code2))
      return getWeather(code2);

    return ["🌧️","Βροχή"];
  }

  /*
    No precipitation:
    use the model weather code.
  */

  if(code1 === code2)
    return getWeather(code1);

  /*
    If they differ, prefer the more
    conservative cloud condition.
  */

  const priority = {
    0:0,
    1:1,
    2:2,
    3:3
  };

  if(
    priority[code1] != null &&
    priority[code2] != null
  ){

    return priority[code1] >= priority[code2]
      ? getWeather(code1)
      : getWeather(code2);
  }

  return getWeather(code1);
}


/* =========================================================
   15-DAY FORECAST
========================================================= */

function renderForecast(
  ifs,
  aifs
){

  const container =
    document.getElementById(
      "forecast"
    );

  const fragment =
    document.createDocumentFragment();

  const count =
    Math.min(
      15,
      ifs.daily.time.length,
      aifs.daily.time.length
    );

  for(let i=0;i<count;i++){

    const high =
      average(
        ifs.daily.temperature_2m_max[i],
        aifs.daily.temperature_2m_max[i]
      );

    const low =
      average(
        ifs.daily.temperature_2m_min[i],
        aifs.daily.temperature_2m_min[i]
      );

    const precipitation =
      average(
        ifs.daily.precipitation_sum[i],
        aifs.daily.precipitation_sum[i]
      );

    const rain =
      average(
        ifs.daily.rain_sum[i],
        aifs.daily.rain_sum[i]
      );

    const snow =
      average(
        ifs.daily.snowfall_sum[i],
        aifs.daily.snowfall_sum[i]
      );

    const condition =
      conditionFromModels(
        ifs.daily.weather_code[i],
        aifs.daily.weather_code[i],
        rain,
        snow
      );

    const date =
      new Date(
        ifs.daily.time[i] +
        "T12:00:00"
      );

    const dateText =
      date.toLocaleDateString(
        "el-GR",
        {
          weekday:"short",
          day:"numeric",
          month:"short"
        }
      );

    const card =
      document.createElement("div");

    card.className =
      "day glass";

    card.innerHTML = `

      <div class="day-date">
        ${dateText}
      </div>

      <div class="day-icon">
        ${condition[0]}
      </div>

      <div class="day-condition">
        ${condition[1]}
      </div>

      <div class="temps">

        <div class="temp-high">
          ${Math.round(high)}°
        </div>

        <div class="temp-low">
          ${Math.round(low)}°
        </div>

      </div>

      <div class="rain">
        💧 ${Number(precipitation || 0).toFixed(1)} mm
      </div>

      ${
        Number(snow) > 0.05
        ?
        `
        <div class="snow">
          ❄️ ${Number(snow).toFixed(1)} cm
        </div>
        `
        :
        ""
      }

    `;

    fragment.appendChild(card);
  }

  container.replaceChildren(
    fragment
  );
}


/* =========================================================
   MAP
========================================================= */

function initializeMap(){

  map =
    L.map(
      "map",
      {
        zoomControl:true,
        preferCanvas:true
      }
    ).setView(
      [
        selectedLat,
        selectedLon
      ],
      7
    );

  L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
      maxZoom:19,
      attribution:
        "&copy; OpenStreetMap contributors",
      updateWhenIdle:true,
      keepBuffer:1
    }
  ).addTo(map);

  marker =
    L.marker([
      selectedLat,
      selectedLon
    ]).addTo(map);

  marker.bindPopup(
    selectedName
  );
}


function updateMap(){

  if(!map || !marker)
    return;

  marker.setLatLng([
    selectedLat,
    selectedLon
  ]);

  marker.setPopupContent(
    selectedName
  );

  map.setView(
    [
      selectedLat,
      selectedLon
    ],
    8,
    {
      animate:false
    }
  );

  /*
    Leaflet can calculate the container size
    incorrectly when the page is still rendering.
  */

  requestAnimationFrame(
    ()=>{
      map.invalidateSize(false);
    }
  );
}


/* =========================================================
   LOAD LOCATION
========================================================= */

async function loadLocation(
  name,
  lat,
  lon
){

  /*
    Give every request its own ID.
    Old responses can never overwrite a newer search.
  */

  const myRequest =
    ++requestId;

  /*
    Abort the previous request immediately.
  */

  if(controller){
    controller.abort();
  }

  controller =
    new AbortController();

  selectedName =
    String(name);

  selectedLat =
    Number(lat);

  selectedLon =
    Number(lon);

  if(
    !Number.isFinite(selectedLat) ||
    !Number.isFinite(selectedLon)
  ){
    return;
  }

  document.getElementById(
    "locationName"
  ).textContent =
    selectedName;

  document.getElementById(
    "status"
  ).textContent =
    "Φόρτωση πραγματικών δεδομένων ECMWF...";

  try{

    const models =
      await loadModels(
        selectedLat,
        selectedLon,
        controller.signal
      );

    /*
      Another search may have happened
      while we were waiting.
    */

    if(
      myRequest !== requestId
    ){
      return;
    }

    renderCurrent(
      models.ifs,
      models.aifs
    );

    renderForecast(
      models.ifs,
      models.aifs
    );

    updateMap();

    document.getElementById(
      "status"
    ).textContent =
      "ECMWF IFS HRES 9 km + AIFS • μέσος όρος μοντέλων";

  }
  catch(error){

    /*
      Abort is normal when the user searches
      for another place.
    */

    if(
      error.name === "AbortError"
    ){
      return;
    }

    console.error(error);

    document.getElementById(
      "status"
    ).textContent =
      "Δεν ήταν δυνατή η φόρτωση των δεδομένων. Δοκίμασε ξανά.";
  }
}


/* =========================================================
   SEARCH
========================================================= */

async function searchPlace(){

  const input =
    document.getElementById(
      "searchInput"
    );

  const button =
    document.getElementById(
      "searchButton"
    );

  const results =
    document.getElementById(
      "results"
    );

  const query =
    input.value.trim();

  if(query.length < 2){

    document.getElementById(
      "status"
    ).textContent =
      "Γράψε τουλάχιστον 2 χαρακτήρες.";

    return;
  }

  button.disabled = true;

  results.replaceChildren();
  results.style.display = "none";

  document.getElementById(
    "status"
  ).textContent =
    "Αναζήτηση υπαρκτών τοποθεσιών...";

  try{

    /*
      Up to 20 real matches.
      The user can select the correct one.
    */

    const url =
      "https://geocoding-api.open-meteo.com/v1/search" +

      "?name=" +
      encodeURIComponent(query) +

      "&count=20" +

      "&language=el" +

      "&format=json";

    const response =
      await fetch(
        url,
        {
          cache:"no-store"
        }
      );

    if(!response.ok)
      throw new Error(
        "Geocoding failed"
      );

    const data =
      await response.json();

    if(
      !data.results ||
      data.results.length === 0
    ){

      document.getElementById(
        "status"
      ).textContent =
        "Δεν βρέθηκε υπαρκτή τοποθεσία με αυτό το όνομα.";

      return;
    }

    /*
      One exact result:
      load immediately.
    */

    if(data.results.length === 1){

      const place =
        data.results[0];

      await loadLocation(
        formatPlace(place),
        place.latitude,
        place.longitude
      );

      return;
    }

    /*
      Multiple results:
      show actual locations.
    */

    data.results.forEach(
      place=>{

        const resultButton =
          document.createElement(
            "button"
          );

        resultButton.className =
          "result-btn";

        resultButton.textContent =
          formatPlace(place);

        resultButton.onclick =
          function(){

            results.style.display =
              "none";

            loadLocation(
              formatPlace(place),
              place.latitude,
              place.longitude
            );

          };

        results.appendChild(
          resultButton
        );
      }
    );

    results.style.display =
      "flex";

    document.getElementById(
      "status"
    ).textContent =
      "Βρέθηκαν " +
      data.results.length +
      " υπαρκτές τοποθεσίες. Επίλεξε τη σωστή.";

  }
  catch(error){

    console.error(error);

    document.getElementById(
      "status"
    ).textContent =
      "Σφάλμα στην αναζήτηση. Δοκίμασε ξανά.";

  }
  finally{

    button.disabled = false;

  }
}


/* =========================================================
   FORMAT SEARCH RESULT
========================================================= */

function formatPlace(place){

  const parts = [];

  if(place.name)
    parts.push(place.name);

  if(place.admin1 &&
     place.admin1 !== place.name)
    parts.push(place.admin1);

  if(place.country)
    parts.push(place.country);

  return parts.join(" • ");
}


/* =========================================================
   ENTER KEY
========================================================= */

document
  .getElementById("searchInput")
  .addEventListener(
    "keydown",
    function(event){

      if(event.key === "Enter"){

        event.preventDefault();

        searchPlace();
      }

    }
  );


/* =========================================================
   START
========================================================= */

window.addEventListener(
  "load",
  function(){

    initializeMap();

    /*
      Let the browser paint the interface
      before starting the API requests.
    */

    requestAnimationFrame(
      function(){

        loadLocation(
          "Θεσσαλονίκη",
          40.6401,
          22.9444
        );

      }
    );

  }
);

</script>

</body>
</html>
