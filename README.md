<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>The Greece Weather</title>

<link
  rel="stylesheet"
  href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
/>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  color: white;
  background:
    radial-gradient(circle at top left, #174d82 0%, transparent 35%),
    linear-gradient(135deg, #06152b, #0b2949 55%, #071526);
  min-height: 100vh;
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
  margin-bottom: 18px;
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

.search-box button:hover {
  background: #3799e9;
}

.cities {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.city-btn {
  border: 1px solid rgba(255,255,255,0.15);
  background: rgba(255,255,255,0.08);
  color: white;
  padding: 9px 14px;
  border-radius: 999px;
  cursor: pointer;
}

.city-btn:hover {
  background: rgba(255,255,255,0.16);
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
  line-height: 1.25;
}

/* ΘΕΡΜΟΚΡΑΣΙΕΣ ΠΑΝΩ-ΚΑΤΩ */
.temps {
  margin-top: 13px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
  font-size: 20px;
  font-weight: bold;
}

.temp-high {
  font-size: 20px;
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
  background: #dbe8f2;
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
  <h1>🌍 The Greece Weather</h1>
  <p>ECMWF IFS HRES 9 km + ECMWF AIFS</p>
</header>

<div class="search-box glass">
  <input
    id="searchInput"
    type="text"
    placeholder="Αναζήτησε πόλη ή περιοχή σε όλο τον κόσμο..."
    autocomplete="off"
  >
  <button onclick="searchPlace()">Αναζήτηση</button>
</div>

<div class="cities">

  <button class="city-btn"
    onclick="loadCity('Αθήνα',37.9838,23.7275)">
    Αθήνα
  </button>

  <button class="city-btn"
    onclick="loadCity('Θεσσαλονίκη',40.6401,22.9444)">
    Θεσσαλονίκη
  </button>

  <button class="city-btn"
    onclick="loadCity('Πάτρα',38.2466,21.7346)">
    Πάτρα
  </button>

  <button class="city-btn"
    onclick="loadCity('Λάρισα',39.6390,22.4191)">
    Λάρισα
  </button>

  <button class="city-btn"
    onclick="loadCity('Ηράκλειο',35.3387,25.1442)">
    Ηράκλειο
  </button>

  <button class="city-btn"
    onclick="loadCity('Ιωάννινα',39.6650,20.8537)">
    Ιωάννινα
  </button>

  <button class="city-btn"
    onclick="loadCity('Καβάλα',40.9396,24.4018)">
    Καβάλα
  </button>

  <button class="city-btn"
    onclick="loadCity('Ρόδος',36.4349,28.2176)">
    Ρόδος
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
   ΒΑΣΙΚΑ
========================================================= */

let selectedLat = 40.6401;
let selectedLon = 22.9444;
let selectedName = "Θεσσαλονίκη";

let map;
let marker;


/* =========================================================
   WEATHER CODES
========================================================= */

const weatherCodes = {

  0:  ["☀️", "Καθαρός ουρανός"],
  1:  ["🌤️", "Κυρίως αίθριος"],
  2:  ["⛅", "Μερική συννεφιά"],
  3:  ["☁️", "Συννεφιά"],

  45: ["🌫️", "Ομίχλη"],
  48: ["🌫️", "Ομίχλη με πάχνη"],

  51: ["🌦️", "Ασθενές ψιλόβροχο"],
  53: ["🌦️", "Μέτριο ψιλόβροχο"],
  55: ["🌧️", "Ισχυρό ψιλόβροχο"],

  56: ["🌧️❄️", "Παγωμένο ψιλόβροχο"],
  57: ["🌧️❄️", "Ισχυρό παγωμένο ψιλόβροχο"],

  61: ["🌧️", "Ασθενής βροχή"],
  63: ["🌧️", "Μέτρια βροχή"],
  65: ["🌧️", "Ισχυρή βροχή"],

  66: ["🌧️❄️", "Παγωμένη βροχή"],
  67: ["🌧️❄️", "Ισχυρή παγωμένη βροχή"],

  71: ["🌨️", "Ασθενής χιονόπτωση"],
  73: ["❄️", "Μέτρια χιονόπτωση"],
  75: ["❄️", "Ισχυρή χιονόπτωση"],

  77: ["❄️", "Κόκκοι χιονιού"],

  80: ["🌦️", "Ασθενείς μπόρες"],
  81: ["🌧️", "Μέτριες μπόρες"],
  82: ["⛈️", "Ισχυρές μπόρες"],

  85: ["🌨️", "Ασθενείς χιονομπόρες"],
  86: ["🌨️", "Ισχυρές χιονομπόρες"],

  95: ["⛈️", "Καταιγίδα"],
  96: ["⛈️", "Καταιγίδα με χαλάζι"],
  99: ["⛈️", "Ισχυρή καταιγίδα με χαλάζι"]
};


function getWeather(code) {

  return weatherCodes[code] ||
    ["🌡️", "Μεταβλητός καιρός"];

}


/* =========================================================
   ΣΩΣΤΟΣ ΧΕΙΡΙΣΜΟΣ ΒΡΟΧΗΣ / ΧΙΟΝΙΟΥ
========================================================= */

function chooseWeatherCode(
  code1,
  code2,
  rain1,
  rain2,
  snow1,
  snow2
) {

  const snow = (snow1 || 0) + (snow2 || 0);
  const rain = (rain1 || 0) + (rain2 || 0);

  if (snow > 0.05 && rain > 0.05) {

    return {
      icon: "🌧️❄️",
      text: "Μικτός υετός"
    };

  }

  if (snow > 0.05) {

    const snowCodes = [
      71,73,75,77,85,86
    ];

    if (snowCodes.includes(code1)) {

      const w = getWeather(code1);

      return {
        icon: w[0],
        text: w[1]
      };

    }

    if (snowCodes.includes(code2)) {

      const w = getWeather(code2);

      return {
        icon: w[0],
        text: w[1]
      };

    }

    return {
      icon: "❄️",
      text: "Χιονόπτωση"
    };

  }

  if (rain > 0.05) {

    const rainCodes = [
      51,53,55,
      56,57,
      61,63,65,
      66,67,
      80,81,82,
      95,96,99
    ];

    if (rainCodes.includes(code1)) {

      const w = getWeather(code1);

      return {
        icon: w[0],
        text: w[1]
      };

    }

    if (rainCodes.includes(code2)) {

      const w = getWeather(code2);

      return {
        icon: w[0],
        text: w[1]
      };

    }

    return {
      icon: "🌧️",
      text: "Βροχή"
    };

  }

  if (code1 === code2) {

    const w = getWeather(code1);

    return {
      icon: w[0],
      text: w[1]
    };

  }

  const w = getWeather(code1);

  return {
    icon: w[0],
    text: w[1]
  };

}


/* =========================================================
   ΜΕΣΟΣ ΟΡΟΣ
========================================================= */

function avg(a, b) {

  if (a == null && b == null)
    return null;

  if (a == null)
    return b;

  if (b == null)
    return a;

  return (a + b) / 2;

}


/* =========================================================
   ΚΥΚΛΙΚΟΣ ΜΕΣΟΣ ΑΝΕΜΟΥ
========================================================= */

function averageWindDirection(a, b) {

  if (a == null && b == null)
    return null;

  if (a == null)
    return b;

  if (b == null)
    return a;

  const ar = a * Math.PI / 180;
  const br = b * Math.PI / 180;

  const x =
    Math.cos(ar) +
    Math.cos(br);

  const y =
    Math.sin(ar) +
    Math.sin(br);

  let degrees =
    Math.atan2(y, x) *
    180 / Math.PI;

  if (degrees < 0)
    degrees += 360;

  return degrees;

}


/* =========================================================
   ΔΙΕΥΘΥΝΣΗ
========================================================= */

function windDirection(degrees) {

  if (degrees == null)
    return "--";

  const dirs = [
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

  const index =
    Math.round(degrees / 22.5) % 16;

  return dirs[index];

}


/* =========================================================
   API
========================================================= */

async function getModel(
  model,
  lat,
  lon
) {

  const url =
    "https://api.open-meteo.com/v1/forecast" +

    "?latitude=" +
    encodeURIComponent(lat) +

    "&longitude=" +
    encodeURIComponent(lon) +

    "&models=" +
    encodeURIComponent(model) +

    "&current=" +
    "temperature_2m," +
    "relative_humidity_2m," +
    "wind_speed_10m," +
    "wind_direction_10m," +
    "weather_code" +

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

  const response =
    await fetch(url);

  if (!response.ok) {
    throw new Error("Weather API error");
  }

  return await response.json();

}


/* =========================================================
   MODELS
========================================================= */

async function getBothModels(
  lat,
  lon
) {

  const [
    ifs,
    aifs
  ] = await Promise.all([

    getModel(
      "ecmwf_ifs025",
      lat,
      lon
    ),

    getModel(
      "ecmwf_aifs025",
      lat,
      lon
    )

  ]);

  return {
    ifs,
    aifs
  };

}


/* =========================================================
   CURRENT
========================================================= */

function renderCurrent(
  ifs,
  aifs
) {

  const temp =
    avg(
      ifs.current.temperature_2m,
      aifs.current.temperature_2m
    );

  const humidity =
    avg(
      ifs.current.relative_humidity_2m,
      aifs.current.relative_humidity_2m
    );

  const wind =
    avg(
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
    Math.round(temp) + "°";

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
   15ΗΜΕΡΟ
========================================================= */

function renderForecast(
  ifs,
  aifs
) {

  const container =
    document.getElementById(
      "forecast"
    );

  container.innerHTML = "";

  const days =
    ifs.daily.time;

  for (
    let i = 0;
    i < 15;
    i++
  ) {

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

    const condition =
      chooseWeatherCode(

        ifs.daily.weather_code[i],
        aifs.daily.weather_code[i],

        rain,
        rain,

        snow,
        snow

      );

    const date =
      new Date(
        days[i] + "T12:00:00"
      );

    const dateText =
      date.toLocaleDateString(
        "el-GR",
        {
          weekday: "short",
          day: "numeric",
          month: "short"
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
        ${condition.icon}
      </div>

      <div class="day-condition">
        ${condition.text}
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
        💧 ${precipitation.toFixed(1)} mm
      </div>

      ${
        snow > 0.05
        ?
        `
        <div class="snow">
          ❄️ ${snow.toFixed(1)} cm
        </div>
        `
        :
        ""
      }

    `;

    container.appendChild(card);

  }

}


/* =========================================================
   MAP
========================================================= */

function initializeMap() {

  map =
    L.map(
      "map",
      {
        zoomControl: true
      }
    ).setView(
      [
        selectedLat,
        selectedLon
      ],
      7
    );

  /*
    Χρησιμοποιούμε HTTPS tiles.
    Αυτό διορθώνει το πρόβλημα όταν η σελίδα
    είναι σε HTTPS/GitHub Pages.
  */

  L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
      maxZoom: 19,
      attribution:
        '&copy; <a href="https://www.openstreetmap.org/copyright" target="_blank">OpenStreetMap</a>'
    }
  ).addTo(map);

  marker =
    L.marker(
      [
        selectedLat,
        selectedLon
      ]
    ).addTo(map);

  marker
    .bindPopup(selectedName)
    .openPopup();

}


/* =========================================================
   UPDATE MAP
========================================================= */

function updateMap() {

  if (!map)
    return;

  map.invalidateSize();

  map.setView(
    [
      selectedLat,
      selectedLon
    ],
    8,
    {
      animate: true
    }
  );

  marker.setLatLng(
    [
      selectedLat,
      selectedLon
    ]
  );

  marker
    .setPopupContent(
      selectedName
    );

}


/* =========================================================
   LOAD LOCATION
========================================================= */

async function loadLocation(
  name,
  lat,
  lon
) {

  selectedName = name;
  selectedLat = Number(lat);
  selectedLon = Number(lon);

  document.getElementById(
    "locationName"
  ).textContent =
    selectedName;

  document.getElementById(
    "status"
  ).textContent =
    "Φόρτωση ECMWF IFS HRES + AIFS...";

  document.getElementById(
    "forecast"
  ).innerHTML = "";

  try {

    const models =
      await getBothModels(
        selectedLat,
        selectedLon
      );

    renderCurrent(
      models.ifs,
      models.aifs
    );

    renderForecast(
      models.ifs,
      models.aifs
    );

    updateMap();

    /*
      Το invalidateSize ξαναϋπολογίζει το μέγεθος
      του Leaflet όταν έχει φορτώσει όλο το περιεχόμενο.
    */

    setTimeout(
      function() {

        if (map) {
          map.invalidateSize();
        }

      },
      300
    );

    document.getElementById(
      "status"
    ).textContent =
      "Τελευταία διαθέσιμα δεδομένα ECMWF";

  } catch (error) {

    console.error(error);

    document.getElementById(
      "status"
    ).textContent =
      "Δεν ήταν δυνατή η φόρτωση των δεδομένων.";

  }

}


/* =========================================================
   QUICK CITY
========================================================= */

function loadCity(
  name,
  lat,
  lon
) {

  loadLocation(
    name,
    lat,
    lon
  );

}


/* =========================================================
   WORLD SEARCH
========================================================= */

async function searchPlace() {

  const input =
    document.getElementById(
      "searchInput"
    );

  const query =
    input.value.trim();

  if (!query)
    return;

  document.getElementById(
    "status"
  ).textContent =
    "Αναζήτηση...";

  try {

    const url =
      "https://geocoding-api.open-meteo.com/v1/search" +

      "?name=" +
      encodeURIComponent(query) +

      "&count=1" +

      "&language=el" +

      "&format=json";

    const response =
      await fetch(url);

    if (!response.ok) {
      throw new Error(
        "Geocoding error"
      );
    }

    const data =
      await response.json();

    if (
      !data.results ||
      !data.results.length
    ) {

      document.getElementById(
        "status"
      ).textContent =
        "Δεν βρέθηκε η περιοχή.";

      return;
    }

    const place =
      data.results[0];

    let fullName =
      place.name || query;

    if (place.country) {

      fullName +=
        ", " +
        place.country;

    }

    await loadLocation(

      fullName,

      place.latitude,

      place.longitude

    );

  } catch (error) {

    console.error(error);

    document.getElementById(
      "status"
    ).textContent =
      "Σφάλμα στην αναζήτηση.";

  }

}


/* =========================================================
   ENTER
========================================================= */

document
  .getElementById(
    "searchInput"
  )
  .addEventListener(
    "keydown",
    function(event) {

      if (
        event.key === "Enter"
      ) {

        searchPlace();

      }

    }
  );


/* =========================================================
   START
========================================================= */

window.addEventListener(
  "load",
  async function() {

    initializeMap();

    await loadLocation(
      "Θεσσαλονίκη",
      40.6401,
      22.9444
    );

  }
);

</script>

</body>
</html>
