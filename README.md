<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>WORLD WEATHER</title>

<link rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

<style>
* {
  box-sizing: border-box;
}

html, body {
  margin: 0;
  min-height: 100%;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  color: white;
  background:
    radial-gradient(circle at top left, #174d82 0%, transparent 35%),
    linear-gradient(135deg, #06152b, #0b2949 55%, #071526);
}

.container {
  width: min(1200px, 94%);
  margin: auto;
  padding: 25px 0 45px;
}

header {
  text-align: center;
  margin-bottom: 25px;
}

header h1 {
  margin: 0;
  font-size: clamp(30px, 6vw, 55px);
  letter-spacing: -1px;
}

header p {
  margin: 8px 0 0;
  color: #bcd5ec;
  font-size: 15px;
}

.glass {
  background: rgba(255,255,255,0.09);
  border: 1px solid rgba(255,255,255,0.13);
  box-shadow: 0 15px 45px rgba(0,0,0,0.25);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  border-radius: 22px;
}

.search-box {
  padding: 18px;
  display: flex;
  gap: 10px;
  margin-bottom: 12px;
}

.search-box input {
  flex: 1;
  min-width: 0;
  padding: 15px 17px;
  border-radius: 14px;
  border: none;
  outline: none;
  background: rgba(255,255,255,0.95);
  color: #10233d;
  font-size: 16px;
}

.search-box button {
  border: none;
  border-radius: 14px;
  padding: 0 22px;
  background: #2788d9;
  color: white;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

.search-box button:disabled {
  opacity: 0.6;
  cursor: wait;
}

.results {
  display: none;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 15px;
}

.result-btn {
  border: 1px solid rgba(255,255,255,0.15);
  background: rgba(255,255,255,0.09);
  color: white;
  padding: 10px 14px;
  border-radius: 14px;
  cursor: pointer;
  text-align: left;
}

.result-btn:hover {
  background: rgba(255,255,255,0.17);
}

.cities {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 18px;
}

.city-btn {
  border: 1px solid rgba(255,255,255,0.15);
  background: rgba(255,255,255,0.08);
  color: white;
  padding: 9px 14px;
  border-radius: 999px;
  cursor: pointer;
}

.status {
  min-height: 24px;
  margin: 5px 3px 15px;
  color: #bcd5ec;
  font-size: 14px;
}

.current {
  padding: 25px;
  margin-bottom: 20px;
}

.location-name {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 20px;
}

.current-temp {
  font-size: clamp(55px, 11vw, 90px);
  font-weight: 700;
  line-height: 1;
  margin-bottom: 20px;
}

.current-details {
  display: flex;
  gap: 18px;
  flex-wrap: wrap;
  color: #dcecff;
  font-size: 16px;
}

.current-details span {
  background: rgba(255,255,255,0.07);
  padding: 9px 12px;
  border-radius: 12px;
}

.section-title {
  margin: 25px 0 13px;
  font-size: 22px;
}

.forecast {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(135px, 1fr));
  gap: 10px;
}

.day {
  padding: 16px 12px;
  text-align: center;
  min-height: 225px;
}

.day-date {
  font-size: 14px;
  color: #bdd5ec;
  margin-bottom: 12px;
}

.day-icon {
  font-size: 38px;
  margin: 7px 0;
}

.day-condition {
  min-height: 35px;
  font-size: 13px;
  color: #dcecff;
}

.temps {
  margin-top: 13px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
}

.temp-high {
  font-size: 20px;
  font-weight: bold;
}

.temp-low {
  font-size: 17px;
  color: #b9d1e8;
}

.rain {
  margin-top: 9px;
  color: #9dd7ff;
  font-size: 13px;
}

.snow {
  margin-top: 4px;
  color: #e3f4ff;
  font-size: 13px;
}

.map-card {
  padding: 14px;
  margin-top: 20px;
}

#map {
  width: 100%;
  height: 400px;
  border-radius: 16px;
  overflow: hidden;
}

.footer {
  text-align: center;
  color: #8eabc5;
  font-size: 12px;
  margin-top: 25px;
}

@media (max-width: 600px) {

  .search-box {
    flex-direction: column;
  }

  .search-box button {
    padding: 14px;
  }

  .forecast {
    grid-template-columns: repeat(2, 1fr);
  }

  #map {
    height: 320px;
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
    placeholder="Αναζήτησε πόλη ή περιοχή οπουδήποτε στον κόσμο..."
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

    <span id="humidity">💧 --%</span>

    <span id="windSpeed">💨 -- km/h</span>

    <span id="windDirection">🧭 --</span>

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

/* =====================================================
   STATE
===================================================== */

let map = null;
let marker = null;

let currentController = null;
let requestId = 0;

let selectedLat = 40.6401;
let selectedLon = 22.9444;
let selectedName = "Θεσσαλονίκη";


/* =====================================================
   WEATHER CODES
===================================================== */

const weatherCodes = {

  0: ["☀️","Καθαρός ουρανός"],
  1: ["🌤️","Κυρίως αίθριος"],
  2: ["⛅","Μερική συννεφιά"],
  3: ["☁️","Συννεφιά"],

  45: ["🌫️","Ομίχλη"],
  48: ["🌫️","Ομίχλη"],

  51: ["🌦️","Ασθενές ψιλόβροχο"],
  53: ["🌦️","Μέτριο ψιλόβροχο"],
  55: ["🌧️","Ισχυρό ψιλόβροχο"],

  56: ["🌧️❄️","Παγωμένο ψιλόβροχο"],
  57: ["🌧️❄️","Ισχυρό παγωμένο ψιλόβροχο"],

  61: ["🌧️","Ασθενής βροχή"],
  63: ["🌧️","Μέτρια βροχή"],
  65: ["🌧️","Ισχυρή βροχή"],

  66: ["🌧️❄️","Παγωμένη βροχή"],
  67: ["🌧️❄️","Ισχυρή παγωμένη βροχή"],

  71: ["🌨️","Ασθενής χιονόπτωση"],
  73: ["❄️","Μέτρια χιονόπτωση"],
  75: ["❄️","Ισχυρή χιονόπτωση"],

  77: ["❄️","Κόκκοι χιονιού"],

  80: ["🌦️","Ασθενείς μπόρες"],
  81: ["🌧️","Μέτριες μπόρες"],
  82: ["⛈️","Ισχυρές μπόρες"],

  85: ["🌨️","Ασθενείς χιονομπόρες"],
  86: ["🌨️","Ισχυρές χιονομπόρες"],

  95: ["⛈️","Καταιγίδα"],
  96: ["⛈️","Καταιγίδα με χαλάζι"],
  99: ["⛈️","Ισχυρή καταιγίδα με χαλάζι"]

};


/* =====================================================
   HELPERS
===================================================== */

function avg(a,b) {

  if (a == null && b == null) return null;
  if (a == null) return b;
  if (b == null) return a;

  return (a+b)/2;
}


function averageDirection(a,b) {

  if (a == null && b == null) return null;
  if (a == null) return b;
  if (b == null) return a;

  const ar = a * Math.PI / 180;
  const br = b * Math.PI / 180;

  const x = Math.cos(ar) + Math.cos(br);
  const y = Math.sin(ar) + Math.sin(br);

  let result = Math.atan2(y,x) * 180 / Math.PI;

  if (result < 0) result += 360;

  return result;
}


function windDirection(degrees) {

  if (degrees == null) return "--";

  const dirs = [
    "Β","ΒΒΑ","ΒΑ","ΑΒΑ",
    "Α","ΑΝΑ","ΝΑ","ΝΝΑ",
    "Ν","ΝΝΔ","ΝΔ","ΔΝΔ",
    "Δ","ΔΒΔ","ΒΔ","ΒΒΔ"
  ];

  return dirs[
    Math.round(degrees / 22.5) % 16
  ];
}


function weather(code) {

  return weatherCodes[code] ||
    ["🌡️","Μεταβλητός καιρός"];

}


/* =====================================================
   REAL ECMWF MODEL REQUEST
===================================================== */

async function getIFS(lat,lon,signal) {

  const url =
    "https://api.open-meteo.com/v1/ecmwf" +

    "?latitude=" + encodeURIComponent(lat) +
    "&longitude=" + encodeURIComponent(lon) +

    "&hourly=" +
    "temperature_2m," +
    "relative_humidity_2m," +
    "wind_speed_10m," +
    "wind_direction_10m," +
    "weather_code," +
    "precipitation," +
    "rain," +
    "snowfall" +

    "&daily=" +
    "temperature_2m_max," +
    "temperature_2m_min," +
    "precipitation_sum," +
    "rain_sum," +
    "snowfall_sum," +
    "weather_code" +

    "&forecast_days=15" +
    "&timezone=auto" +
    "&temperature_unit=celsius" +
    "&wind_speed_unit=kmh" +
    "&precipitation_unit=mm";

  const response = await fetch(url,{
    signal: signal
  });

  if (!response.ok)
    throw new Error("IFS request failed");

  return await response.json();
}


/* =====================================================
   REAL ECMWF AIFS REQUEST
===================================================== */

async function getAIFS(lat,lon,signal) {

  const url =
    "https://api.open-meteo.com/v1/forecast" +

    "?latitude=" + encodeURIComponent(lat) +
    "&longitude=" + encodeURIComponent(lon) +

    "&models=ecmwf_aifs025" +

    "&hourly=" +
    "temperature_2m," +
    "relative_humidity_2m," +
    "wind_speed_10m," +
    "wind_direction_10m," +
    "weather_code," +
    "precipitation," +
    "rain," +
    "snowfall" +

    "&daily=" +
    "temperature_2m_max," +
    "temperature_2m_min," +
    "precipitation_sum," +
    "rain_sum," +
    "snowfall_sum," +
    "weather_code" +

    "&forecast_days=15" +
    "&timezone=auto" +
    "&temperature_unit=celsius" +
    "&wind_speed_unit=kmh" +
    "&precipitation_unit=mm";

  const response = await fetch(url,{
    signal: signal
  });

  if (!response.ok)
    throw new Error("AIFS request failed");

  return await response.json();
}


/* =====================================================
   CURRENT WEATHER
===================================================== */

function renderCurrent(ifs,aifs) {

  const now = new Date();

  /*
    Find the current hour in each model.
  */

  const ifsIndex = findCurrentHour(
    ifs.hourly.time
  );

  const aifsIndex = findCurrentHour(
    aifs.hourly.time
  );

  const temp = avg(
    ifs.hourly.temperature_2m[ifsIndex],
    aifs.hourly.temperature_2m[aifsIndex]
  );

  const humidity = avg(
    ifs.hourly.relative_humidity_2m[ifsIndex],
    aifs.hourly.relative_humidity_2m[aifsIndex]
  );

  const wind = avg(
    ifs.hourly.wind_speed_10m[ifsIndex],
    aifs.hourly.wind_speed_10m[aifsIndex]
  );

  const direction = averageDirection(
    ifs.hourly.wind_direction_10m[ifsIndex],
    aifs.hourly.wind_direction_10m[aifsIndex]
  );

  document.getElementById("currentTemp")
    .textContent = Math.round(temp) + "°";

  document.getElementById("humidity")
    .textContent =
    "💧 " + Math.round(humidity) + "%";

  document.getElementById("windSpeed")
    .textContent =
    "💨 " + Math.round(wind) + " km/h";

  document.getElementById("windDirection")
    .textContent =
    "🧭 " + windDirection(direction);
}


function findCurrentHour(times) {

  const now = new Date();

  let best = 0;
  let bestDifference = Infinity;

  for (let i=0; i<times.length; i++) {

    const time = new Date(times[i]);
    const difference =
      Math.abs(time-now);

    if (difference < bestDifference) {
      bestDifference = difference;
      best = i;
    }
  }

  return best;
}


/* =====================================================
   WEATHER CHOICE
===================================================== */

function chooseCondition(
  code1,
  code2,
  rain,
  snow
) {

  if (snow > 0.05) {

    if (
      [71,73,75,77,85,86]
      .includes(code1)
    ) {
      return weather(code1);
    }

    if (
      [71,73,75,77,85,86]
      .includes(code2)
    ) {
      return weather(code2);
    }

    return ["❄️","Χιονόπτωση"];
  }

  if (rain > 0.05) {

    if (code1 >= 51) {
      return weather(code1);
    }

    if (code2 >= 51) {
      return weather(code2);
    }

    return ["🌧️","Βροχή"];
  }

  if (code1 === code2)
    return weather(code1);

  return weather(code1);
}


/* =====================================================
   15 DAY FORECAST
===================================================== */

function renderForecast(ifs,aifs) {

  const container =
    document.getElementById("forecast");

  const fragment =
    document.createDocumentFragment();

  for (let i=0; i<15; i++) {

    const max = avg(
      ifs.daily.temperature_2m_max[i],
      aifs.daily.temperature_2m_max[i]
    );

    const min = avg(
      ifs.daily.temperature_2m_min[i],
      aifs.daily.temperature_2m_min[i]
    );

    const precipitation = avg(
      ifs.daily.precipitation_sum[i],
      aifs.daily.precipitation_sum[i]
    );

    const rain = avg(
      ifs.daily.rain_sum[i],
      aifs.daily.rain_sum[i]
    );

    const snow = avg(
      ifs.daily.snowfall_sum[i],
      aifs.daily.snowfall_sum[i]
    );

    const condition =
      chooseCondition(
        ifs.daily.weather_code[i],
        aifs.daily.weather_code[i],
        rain,
        snow
      );

    const date =
      new Date(
        ifs.daily.time[i] + "T12:00:00"
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

    card.className = "day glass";

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
          ${Math.round(max)}°
        </div>

        <div class="temp-low">
          ${Math.round(min)}°
        </div>
      </div>

      <div class="rain">
        💧 ${Number(precipitation || 0).toFixed(1)} mm
      </div>

      ${
        snow > 0.05
        ?
        `<div class="snow">
          ❄️ ${Number(snow).toFixed(1)} cm
        </div>`
        :
        ""
      }

    `;

    fragment.appendChild(card);
  }

  container.replaceChildren(fragment);
}


/* =====================================================
   MAP
===================================================== */

function initializeMap() {

  map =
    L.map("map",{
      zoomControl:true,
      preferCanvas:true
    }).setView(
      [selectedLat,selectedLon],
      7
    );

  L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
      maxZoom:19,
      attribution:
        "&copy; OpenStreetMap contributors",
      updateWhenIdle:true,
      keepBuffer:2
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


function updateMap() {

  if (!map) return;

  map.setView(
    [selectedLat,selectedLon],
    8,
    {
      animate:false
    }
  );

  marker.setLatLng([
    selectedLat,
    selectedLon
  ]);

  marker.setPopupContent(
    selectedName
  );

  setTimeout(()=>{
    map.invalidateSize(false);
  },100);
}


/* =====================================================
   LOAD LOCATION
===================================================== */

async function loadLocation(
  name,
  lat,
  lon
) {

  const myRequest =
    ++requestId;

  /*
    Cancel previous weather request.
    This is one of the main fixes
    for the freezing problem.
  */

  if (currentController) {
    currentController.abort();
  }

  currentController =
    new AbortController();

  selectedName = name;
  selectedLat = Number(lat);
  selectedLon = Number(lon);

  document.getElementById(
    "locationName"
  ).textContent = selectedName;

  document.getElementById(
    "status"
  ).textContent =
    "Φόρτωση πραγματικών δεδομένων ECMWF...";

  try {

    /*
      IFS and AIFS load simultaneously,
      but the previous search is cancelled.
    */

    const [
      ifs,
      aifs
    ] = await Promise.all([
      getIFS(
        selectedLat,
        selectedLon,
        currentController.signal
      ),

      getAIFS(
        selectedLat,
        selectedLon,
        currentController.signal
      )
    ]);

    /*
      Ignore an older request even if
      the browser completed it first.
    */

    if (myRequest !== requestId)
      return;

    renderCurrent(
      ifs,
      aifs
    );

    renderForecast(
      ifs,
      aifs
    );

    updateMap();

    document.getElementById(
      "status"
    ).textContent =
      "Πραγματικά δεδομένα ECMWF • IFS HRES 9 km + AIFS";

  }
  catch(error) {

    if (
      error.name === "AbortError"
    ) {
      return;
    }

    console.error(error);

    document.getElementById(
      "status"
    ).textContent =
      "Δεν ήταν δυνατή η φόρτωση της πρόγνωσης. Δοκίμασε ξανά.";

  }
}


/* =====================================================
   WORLD SEARCH
===================================================== */

async function searchPlace() {

  const input =
    document.getElementById(
      "searchInput"
    );

  const button =
    document.getElementById(
      "searchButton"
    );

  const resultsBox =
    document.getElementById(
      "results"
    );

  const query =
    input.value.trim();

  if (!query)
    return;

  button.disabled = true;

  resultsBox.innerHTML = "";
  resultsBox.style.display = "none";

  document.getElementById(
    "status"
  ).textContent =
    "Αναζήτηση τοποθεσίας σε όλο τον κόσμο...";

  try {

    const url =
      "https://geocoding-api.open-meteo.com/v1/search" +

      "?name=" +
      encodeURIComponent(query) +

      "&count=10" +

      "&language=el" +

      "&format=json";

    const response =
      await fetch(url);

    if (!response.ok)
      throw new Error("Geocoding failed");

    const data =
      await response.json();

    if (
      !data.results ||
      data.results.length === 0
    ) {

      document.getElementById(
        "status"
      ).textContent =
        "Δεν βρέθηκε υπαρκτή τοποθεσία με αυτό το όνομα.";

      return;
    }

    /*
      If there is exactly one result,
      load it immediately.
    */

    if (data.results.length === 1) {

      const place =
        data.results[0];

      await loadLocation(
        formatPlaceName(place),
        place.latitude,
        place.longitude
      );

      return;
    }

    /*
      Multiple real locations:
      show choices so the user can select
      the correct one.
    */

    data.results.forEach(
      place => {

        const button =
          document.createElement("button");

        button.className =
          "result-btn";

        button.textContent =
          formatPlaceName(place);

        button.onclick =
          async function() {

            resultsBox.style.display =
              "none";

            await loadLocation(
              formatPlaceName(place),
              place.latitude,
              place.longitude
            );

          };

        resultsBox.appendChild(button);
      }
    );

    resultsBox.style.display =
      "flex";

    document.getElementById(
      "status"
    ).textContent =
      "Βρέθηκαν " +
      data.results.length +
      " υπαρκτές τοποθεσίες. Διάλεξε τη σωστή.";

  }
  catch(error) {

    console.error(error);

    document.getElementById(
      "status"
    ).textContent =
      "Πρόβλημα στην αναζήτηση. Δοκίμασε ξανά.";

  }
  finally {

    button.disabled = false;

  }
}


/* =====================================================
   FORMAT PLACE
===================================================== */

function formatPlaceName(place) {

  let text =
    place.name || "Άγνωστη περιοχή";

  const parts = [];

  if (place.admin1)
    parts.push(place.admin1);

  if (place.country)
    parts.push(place.country);

  if (parts.length)
    text +=
      " • " +
      parts.join(", ");

  return text;
}


/* =====================================================
   ENTER KEY
===================================================== */

document
  .getElementById("searchInput")
  .addEventListener(
    "keydown",
    function(event) {

      if (event.key === "Enter") {

        event.preventDefault();

        searchPlace();

      }

    }
  );


/* =====================================================
   START
===================================================== */

window.addEventListener(
  "load",
  function() {

    initializeMap();

    /*
      Let the page render first.
      Then request weather.
    */

    setTimeout(
      function() {

        loadLocation(
          "Θεσσαλονίκη",
          40.6401,
          22.9444
        );

      },
      80
    );

  }
);

</script>

</body>
</html>
