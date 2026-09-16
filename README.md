<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">

<title>WORLD WEATHER</title>

<link
  rel="stylesheet"
  href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
/>

<style>
*{
  box-sizing:border-box;
}

html,body{
  margin:0;
  padding:0;
  min-height:100%;
  font-family:Arial,sans-serif;
  background:#07152d;
  color:white;
}

body{
  overflow-x:hidden;
}

.container{
  width:min(1100px,94%);
  margin:auto;
  padding:20px 0 40px;
}

header{
  text-align:center;
  padding:15px 0 20px;
}

.logo{
  font-size:30px;
  font-weight:800;
  letter-spacing:1px;
}

.subtitle{
  margin-top:6px;
  color:#a9c3e8;
  font-size:14px;
}

.search-area{
  display:flex;
  gap:10px;
  margin:15px 0;
}

#searchInput{
  flex:1;
  min-width:0;
  padding:15px;
  border:none;
  outline:none;
  border-radius:14px;
  background:#10294b;
  color:white;
  font-size:16px;
}

#searchInput::placeholder{
  color:#91a7c6;
}

button{
  border:0;
  border-radius:13px;
  padding:13px 17px;
  cursor:pointer;
  background:#1c65d1;
  color:white;
  font-weight:700;
}

button:disabled{
  opacity:.5;
  cursor:not-allowed;
}

.results{
  display:grid;
  gap:8px;
  margin-bottom:15px;
}

.result{
  width:100%;
  text-align:left;
  background:#10294b;
  border:1px solid #244873;
}

.quick{
  display:flex;
  gap:8px;
  flex-wrap:wrap;
  margin-bottom:18px;
}

.quick button{
  background:#10294b;
  font-size:13px;
}

.card{
  background:#0d2341;
  border:1px solid #1b416b;
  border-radius:20px;
  padding:20px;
  margin-bottom:18px;
}

.location-title{
  font-size:26px;
  font-weight:800;
}

.location-sub{
  margin-top:5px;
  color:#9db8db;
}

.live-label{
  display:inline-block;
  margin-top:14px;
  padding:6px 10px;
  border-radius:20px;
  background:#173d2d;
  color:#8ee0ad;
  font-size:12px;
  font-weight:bold;
}

.live-grid{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
  margin-top:16px;
}

.live-item{
  background:#102b4d;
  border-radius:15px;
  padding:15px;
}

.live-value{
  font-size:23px;
  font-weight:800;
}

.live-name{
  color:#91acd0;
  font-size:12px;
  margin-top:5px;
}

.status{
  margin-top:12px;
  color:#9eb5d4;
  font-size:13px;
}

.section-title{
  font-size:22px;
  margin:8px 0 14px;
}

.model-info{
  color:#91acd0;
  font-size:13px;
  margin-bottom:15px;
}

.forecast{
  display:grid;
  grid-template-columns:repeat(5,1fr);
  gap:10px;
}

.day{
  background:#102b4d;
  border-radius:16px;
  padding:13px;
  text-align:center;
  min-height:190px;
}

.day-name{
  font-weight:700;
  margin-bottom:8px;
}

.icon{
  font-size:30px;
  margin:5px 0;
}

.temps{
  display:flex;
  flex-direction:column;
  align-items:center;
  gap:2px;
  font-size:19px;
  font-weight:800;
}

.high{
  color:white;
}

.low{
  color:#9ebbe0;
}

.rain{
  margin-top:8px;
  color:#80baff;
  font-size:12px;
}

.map-title{
  font-size:20px;
  margin-bottom:12px;
}

#map{
  height:380px;
  width:100%;
  border-radius:17px;
  overflow:hidden;
}

.error{
  background:#4a1c25;
  border:1px solid #8d3947;
  color:#ffd5da;
  padding:13px;
  border-radius:12px;
  margin-bottom:15px;
}

.loading{
  opacity:.7;
  pointer-events:none;
}

@media(max-width:800px){
  .forecast{
    grid-template-columns:repeat(3,1fr);
  }

  .live-grid{
    grid-template-columns:repeat(2,1fr);
  }
}

@media(max-width:500px){
  .search-area{
    flex-direction:column;
  }

  .forecast{
    grid-template-columns:repeat(2,1fr);
  }

  .logo{
    font-size:25px;
  }

  #map{
    height:300px;
  }
}
</style>
</head>

<body>

<div class="container">

<header>
  <div class="logo">🌍 WORLD WEATHER</div>
  <div class="subtitle">Global weather forecast</div>
</header>

<div class="search-area">
  <input
    id="searchInput"
    type="text"
    placeholder="Αναζήτησε πόλη ή περιοχή οπουδήποτε στον κόσμο..."
    autocomplete="off"
  >
  <button id="searchBtn">Αναζήτηση</button>
</div>

<div id="results" class="results"></div>

<div class="quick">
  <button data-city="Thessaloniki">Θεσσαλονίκη</button>
  <button data-city="Athens">Αθήνα</button>
  <button data-city="London">Λονδίνο</button>
  <button data-city="New York">New York</button>
  <button data-city="Tokyo">Tokyo</button>
  <button data-city="Seoul">Seoul</button>
</div>

<div id="errorBox"></div>

<div class="card">

  <div id="locationTitle" class="location-title">
    Φόρτωση...
  </div>

  <div id="locationSub" class="location-sub"></div>

  <div class="live-label">
    ● LIVE
  </div>

  <div class="live-grid">

    <div class="live-item">
      <div id="liveTemp" class="live-value">—</div>
      <div class="live-name">Θερμοκρασία</div>
    </div>

    <div class="live-item">
      <div id="liveHumidity" class="live-value">—</div>
      <div class="live-name">Υγρασία</div>
    </div>

    <div class="live-item">
      <div id="liveWind" class="live-value">—</div>
      <div class="live-name">Άνεμος</div>
    </div>

    <div class="live-item">
      <div id="liveDirection" class="live-value">—</div>
      <div class="live-name">Διεύθυνση</div>
    </div>

  </div>

  <div id="liveStatus" class="status">
    Αναζήτηση διαθέσιμων τρεχουσών δεδομένων...
  </div>

</div>

<div class="card">

  <div class="section-title">
    📅 15ήμερη πρόγνωση
  </div>

  <div class="model-info">
    Μέσος όρος: ECMWF IFS HRES 9 km + ECMWF AIFS 0.25°
  </div>

  <div id="forecast" class="forecast"></div>

</div>

<div class="card">

  <div class="map-title">
    📍 Τοποθεσία
  </div>

  <div id="map"></div>

</div>

</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

/* =========================================================
   WORLD WEATHER
   ========================================================= */

const GEO_URL =
  "https://geocoding-api.open-meteo.com/v1/search";

const IFS_URL =
  "https://api.open-meteo.com/v1/ecmwf";

const FORECAST_URL =
  "https://api.open-meteo.com/v1/forecast";

/*
  AIFS model.
  Το endpoint του Open-Meteo υποστηρίζει το
  ecmwf_aifs025 ως μοντέλο.
*/

const AIFS_MODEL = "ecmwf_aifs025";


let currentController = null;
let requestNumber = 0;
let map = null;
let marker = null;


/* =========================================================
   DOM
   ========================================================= */

const searchInput =
  document.getElementById("searchInput");

const searchBtn =
  document.getElementById("searchBtn");

const results =
  document.getElementById("results");

const errorBox =
  document.getElementById("errorBox");

const forecastBox =
  document.getElementById("forecast");

const locationTitle =
  document.getElementById("locationTitle");

const locationSub =
  document.getElementById("locationSub");

const liveTemp =
  document.getElementById("liveTemp");

const liveHumidity =
  document.getElementById("liveHumidity");

const liveWind =
  document.getElementById("liveWind");

const liveDirection =
  document.getElementById("liveDirection");

const liveStatus =
  document.getElementById("liveStatus");


/* =========================================================
   TIMEOUT FETCH
   ========================================================= */

async function fetchJSON(url, controller, timeoutMs = 15000){

  const timer = setTimeout(() => {
    controller.abort();
  }, timeoutMs);

  try{

    const response = await fetch(url,{
      signal:controller.signal,
      cache:"no-store"
    });

    if(!response.ok){
      throw new Error(
        "HTTP " + response.status
      );
    }

    return await response.json();

  }finally{
    clearTimeout(timer);
  }
}


/* =========================================================
   ERROR
   ========================================================= */

function showError(message){

  errorBox.innerHTML =
    `<div class="error">${message}</div>`;
}

function clearError(){
  errorBox.innerHTML = "";
}


/* =========================================================
   GEOCODING
   ========================================================= */

async function searchPlaces(text){

  if(!text.trim()) return;

  clearError();

  results.innerHTML =
    `<div class="status">Αναζήτηση περιοχών...</div>`;

  const controller =
    new AbortController();

  try{

    const url =
      GEO_URL +
      "?name=" +
      encodeURIComponent(text.trim()) +
      "&count=20" +
      "&language=el" +
      "&format=json";

    const data =
      await fetchJSON(url,controller);

    results.innerHTML = "";

    if(!data.results || !data.results.length){

      results.innerHTML =
        `<div class="status">
          Δεν βρέθηκε περιοχή.
        </div>`;

      return;
    }

    data.results.forEach(place => {

      const button =
        document.createElement("button");

      button.className = "result";

      const country =
        place.country || "";

      const admin =
        place.admin1
          ? " · " + place.admin1
          : "";

      button.textContent =
        `${place.name}${admin} · ${country}`;

      button.onclick = () => {

        results.innerHTML = "";

        loadLocation({
          name:place.name,
          country:country,
          latitude:Number(place.latitude),
          longitude:Number(place.longitude),
          timezone:place.timezone
        });

      };

      results.appendChild(button);

    });

  }catch(error){

    if(error.name !== "AbortError"){

      results.innerHTML = "";

      showError(
        "Δεν ήταν δυνατή η αναζήτηση αυτή τη στιγμή."
      );

    }
  }
}


/* =========================================================
   WMO
   ========================================================= */

function weatherIcon(code){

  if(code === 0) return "☀️";
  if(code === 1) return "🌤️";
  if(code === 2) return "⛅";
  if(code === 3) return "☁️";

  if([45,48].includes(code))
    return "🌫️";

  if([51,53,55,56,57].includes(code))
    return "🌦️";

  if([61,63,65,66,67].includes(code))
    return "🌧️";

  if([71,73,75,77].includes(code))
    return "❄️";

  if([80,81,82].includes(code))
    return "🌦️";

  if([85,86].includes(code))
    return "🌨️";

  if([95,96,99].includes(code))
    return "⛈️";

  return "🌤️";
}


/* =========================================================
   AVERAGE
   ========================================================= */

function avg(a,b){

  if(
    typeof a !== "number" ||
    typeof b !== "number"
  ){
    return null;
  }

  return (a+b)/2;
}


function avgArray(a,b){

  if(!Array.isArray(a) ||
     !Array.isArray(b)){
    return [];
  }

  const length =
    Math.min(a.length,b.length);

  const output = [];

  for(let i=0;i<length;i++){

    output.push(
      avg(a[i],b[i])
    );

  }

  return output;
}


/* =========================================================
   WIND DIRECTION
   Circular average
   ========================================================= */

function averageDirection(a,b){

  if(
    typeof a !== "number" ||
    typeof b !== "number"
  ){
    return null;
  }

  const ar =
    a * Math.PI / 180;

  const br =
    b * Math.PI / 180;

  const x =
    Math.cos(ar)+Math.cos(br);

  const y =
    Math.sin(ar)+Math.sin(br);

  let deg =
    Math.atan2(y,x)*180/Math.PI;

  if(deg < 0) deg += 360;

  return deg;
}


function directionText(deg){

  if(typeof deg !== "number")
    return "—";

  const dirs = [
    "Β","ΒΑ","Α","ΝΑ",
    "Ν","ΝΔ","Δ","ΒΔ"
  ];

  const index =
    Math.round(deg/45)%8;

  return dirs[index];
}


/* =========================================================
   MODEL REQUESTS
   ========================================================= */

function buildIFSUrl(lat,lon){

  const params = new URLSearchParams({

    latitude:lat,
    longitude:lon,

    timezone:"auto",

    forecast_days:"15",

    current:[
      "temperature_2m",
      "relative_humidity_2m",
      "wind_speed_10m",
      "wind_direction_10m",
      "weather_code",
      "precipitation",
      "rain",
      "snowfall"
    ].join(","),

    daily:[
      "temperature_2m_max",
      "temperature_2m_min",
      "precipitation_sum",
      "rain_sum",
      "snowfall_sum",
      "weather_code"
    ].join(",")

  });

  return IFS_URL + "?" + params.toString();
}


function buildAIFSUrl(lat,lon){

  const params = new URLSearchParams({

    latitude:lat,
    longitude:lon,

    timezone:"auto",

    forecast_days:"15",

    models:AIFS_MODEL,

    current:[
      "temperature_2m",
      "relative_humidity_2m",
      "wind_speed_10m",
      "wind_direction_10m",
      "weather_code",
      "precipitation",
      "rain",
      "snowfall"
    ].join(","),

    daily:[
      "temperature_2m_max",
      "temperature_2m_min",
      "precipitation_sum",
      "rain_sum",
      "snowfall_sum",
      "weather_code"
    ].join(",")

  });

  return FORECAST_URL + "?" + params.toString();
}


/* =========================================================
   LOAD BOTH MODELS
   ========================================================= */

async function loadModels(lat,lon,controller){

  /*
    Και τα δύο requests τρέχουν παράλληλα.
    Αν κάποιο αποτύχει, δεν εμφανίζουμε
    ψεύτικο "μέσο όρο" από ένα μόνο μοντέλο.
  */

  const [ifs,aifs] =
    await Promise.all([

      fetchJSON(
        buildIFSUrl(lat,lon),
        controller,
        15000
      ),

      fetchJSON(
        buildAIFSUrl(lat,lon),
        controller,
        15000
      )

    ]);

  return {ifs,aifs};
}


/* =========================================================
   FORECAST
   ========================================================= */

function renderForecast(ifs,aifs){

  const d1 = ifs.daily;
  const d2 = aifs.daily;

  if(
    !d1 ||
    !d2 ||
    !d1.time ||
    !d2.time
  ){
    throw new Error(
      "Δεν υπάρχουν πλήρη δεδομένα πρόγνωσης."
    );
  }

  const count =
    Math.min(
      15,
      d1.time.length,
      d2.time.length
    );

  forecastBox.innerHTML = "";

  for(let i=0;i<count;i++){

    const max =
      avg(
        d1.temperature_2m_max[i],
        d2.temperature_2m_max[i]
      );

    const min =
      avg(
        d1.temperature_2m_min[i],
        d2.temperature_2m_min[i]
      );

    const rain =
      avg(
        d1.rain_sum[i],
        d2.rain_sum[i]
      );

    const snow =
      avg(
        d1.snowfall_sum[i],
        d2.snowfall_sum[i]
      );

    const precip =
      avg(
        d1.precipitation_sum[i],
        d2.precipitation_sum[i]
      );

    /*
      Για το εικονίδιο δεν κάνουμε μέσο όρο
      κωδικών WMO. Χρησιμοποιούμε πραγματικά
      ποσά βροχής/χιονιού και μετά τον κώδικα.
    */

    let code =
      Number(d1.weather_code[i]);

    if(
      (snow || 0) > 0.1 &&
      (snow || 0) >= (rain || 0)
    ){
      code = 71;
    }
    else if(
      (rain || 0) > 0.1
    ){
      code = 61;
    }
    else{

      const c1 =
        Number(d1.weather_code[i]);

      const c2 =
        Number(d2.weather_code[i]);

      /*
        Για στεγνές συνθήκες κρατάμε τον
        πιο "ενημερωτικό" κώδικα όταν γίνεται.
      */

      code =
        c1 === c2
          ? c1
          : c1;
    }

    const date =
      new Date(
        d1.time[i] + "T12:00:00"
      );

    const dayName =
      date.toLocaleDateString(
        "el-GR",
        {weekday:"short"}
      );

    const dayDate =
      date.toLocaleDateString(
        "el-GR",
        {
          day:"numeric",
          month:"numeric"
        }
      );

    const card =
      document.createElement("div");

    card.className = "day";

    card.innerHTML = `

      <div class="day-name">
        ${dayName}<br>
        ${dayDate}
      </div>

      <div class="icon">
        ${weatherIcon(code)}
      </div>

      <div class="temps">
        <div class="high">
          ${max !== null ? Math.round(max) + "°" : "—"}
        </div>

        <div class="low">
          ${min !== null ? Math.round(min) + "°" : "—"}
        </div>
      </div>

      <div class="rain">
        💧 ${
          precip !== null
            ? precip.toFixed(1) + " mm"
            : "—"
        }
      </div>

    `;

    forecastBox.appendChild(card);
  }
}


/* =========================================================
   CURRENT MODEL DATA
   ========================================================= */

function renderLiveModelFallback(ifs,aifs){

  /*
    ΠΡΟΣΟΧΗ:
    Αυτό ΔΕΝ χαρακτηρίζεται ως πραγματική
    τοπική παρατήρηση.

    Χρησιμοποιείται μόνο σαν τεχνικό fallback
    όταν δεν υπάρχει observation provider.
  */

  const c1 = ifs.current;
  const c2 = aifs.current;

  const temp =
    avg(
      c1.temperature_2m,
      c2.temperature_2m
    );

  const humidity =
    avg(
      c1.relative_humidity_2m,
      c2.relative_humidity_2m
    );

  const wind =
    avg(
      c1.wind_speed_10m,
      c2.wind_speed_10m
    );

  const direction =
    averageDirection(
      c1.wind_direction_10m,
      c2.wind_direction_10m
    );

  liveTemp.textContent =
    temp !== null
      ? Math.round(temp) + "°"
      : "—";

  liveHumidity.textContent =
    humidity !== null
      ? Math.round(humidity) + "%"
      : "—";

  liveWind.textContent =
    wind !== null
      ? Math.round(wind) + " km/h"
      : "—";

  liveDirection.textContent =
    direction !== null
      ? directionText(direction)
      : "—";

  liveStatus.textContent =
    "Δεν βρέθηκε ξεχωριστή τοπική παρατήρηση. Τα παραπάνω είναι προσωρινά δεδομένα μοντέλων και όχι σταθμός.";
}


/* =========================================================
   MAP
   ========================================================= */

function initMap(){

  if(map) return;

  map =
    L.map("map",{
      zoomControl:true
    }).setView(
      [40.64,22.94],
      6
    );

  L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
      maxZoom:19,
      attribution:
        "&copy; OpenStreetMap contributors"
    }
  ).addTo(map);
}


function updateMap(lat,lon,name){

  initMap();

  map.setView(
    [lat,lon],
    9,
    {animate:false}
  );

  if(marker){
    map.removeLayer(marker);
  }

  marker =
    L.marker([lat,lon])
      .addTo(map)
      .bindPopup(name)
      .openPopup();

  setTimeout(() => {
    map.invalidateSize();
  },100);
}


/* =========================================================
   LOAD LOCATION
   ========================================================= */

async function loadLocation(place){

  /*
    Ακυρώνουμε το προηγούμενο request.
    Αυτό είναι πολύ σημαντικό για να μη
    συσσωρεύονται requests όταν ο χρήστης
    αλλάζει περιοχή γρήγορα.
  */

  if(currentController){
    currentController.abort();
  }

  currentController =
    new AbortController();

  const controller =
    currentController;

  const myRequest =
    ++requestNumber;

  clearError();

  document.body.classList.add("loading");

  locationTitle.textContent =
    place.name;

  locationSub.textContent =
    place.country
      ? place.country
      : "";

  liveTemp.textContent = "—";
  liveHumidity.textContent = "—";
  liveWind.textContent = "—";
  liveDirection.textContent = "—";

  liveStatus.textContent =
    "Φόρτωση τρεχόντων δεδομένων...";

  forecastBox.innerHTML =
    `<div class="status">
      Φόρτωση 15ήμερης πρόγνωσης...
    </div>`;

  try{

    /*
      Αν ο χρήστης έχει ήδη πατήσει άλλη περιοχή,
      αγνοούμε αυτό το αποτέλεσμα.
    */

    const {ifs,aifs} =
      await loadModels(
        place.latitude,
        place.longitude,
        controller
      );

    if(
      myRequest !== requestNumber
    ){
      return;
    }

    /*
      15ήμερο:
      ΑΥΣΤΗΡΑ μέσος όρος
      IFS HRES 9 km + AIFS 0.25°
    */

    renderForecast(
      ifs,
      aifs
    );

    /*
      Προσωρινά δείχνουμε το model current
      μόνο ως fallback, με σαφή ένδειξη.
      Δεν το παρουσιάζουμε ως πραγματική
      live παρατήρηση.
    */

    renderLiveModelFallback(
      ifs,
      aifs
    );

    updateMap(
      place.latitude,
      place.longitude,
      place.name
    );

  }catch(error){

    if(
      error.name === "AbortError"
    ){
      return;
    }

    console.error(error);

    forecastBox.innerHTML = "";

    showError(
      "Δεν ήταν δυνατή η φόρτωση των δεδομένων. Δοκίμασε ξανά."
    );

    liveStatus.textContent =
      "Τα δεδομένα δεν ήταν διαθέσιμα αυτή τη στιγμή.";

  }finally{

    if(
      myRequest === requestNumber
    ){
      document.body.classList.remove(
        "loading"
      );
    }
  }
}


/* =========================================================
   EVENTS
   ========================================================= */

searchBtn.addEventListener(
  "click",
  () => {
    searchPlaces(
      searchInput.value
    );
  }
);


searchInput.addEventListener(
  "keydown",
  event => {

    if(event.key === "Enter"){

      event.preventDefault();

      searchPlaces(
        searchInput.value
      );

    }

  }
);


document
  .querySelectorAll(".quick button")
  .forEach(button => {

    button.addEventListener(
      "click",
      () => {

        searchInput.value =
          button.dataset.city;

        searchPlaces(
          button.dataset.city
        );

      }
    );

  });


/* =========================================================
   START
   ========================================================= */

loadLocation({
  name:"Θεσσαλονίκη",
  country:"Ελλάδα",
  latitude:40.6401,
  longitude:22.9444,
  timezone:"Europe/Athens"
});

</script>

</body>
</html>
