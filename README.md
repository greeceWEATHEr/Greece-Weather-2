<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Greece Weather</title>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
  background: linear-gradient(180deg, #0b1d36, #123b68);
  color: white;
  min-height: 100vh;
}

header {
  padding: 25px 20px;
  text-align: center;
  background: rgba(0,0,0,0.2);
}

header h1 {
  font-size: 32px;
}

header p {
  margin-top: 8px;
  opacity: 0.8;
}

.container {
  max-width: 1100px;
  margin: auto;
  padding: 25px 15px;
}

.search {
  display: flex;
  gap: 10px;
  margin-bottom: 25px;
}

.search input {
  flex: 1;
  padding: 15px;
  border: none;
  border-radius: 12px;
  font-size: 16px;
}

.search button {
  padding: 15px 20px;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  font-weight: bold;
}

.current {
  background: rgba(255,255,255,0.12);
  border-radius: 20px;
  padding: 25px;
  margin-bottom: 25px;
  text-align: center;
}

.city {
  font-size: 27px;
  font-weight: bold;
}

.temperature {
  font-size: 65px;
  margin: 15px 0;
}

.condition {
  font-size: 20px;
}

.details {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  margin-top: 20px;
}

.detail {
  background: rgba(255,255,255,0.1);
  padding: 15px;
  border-radius: 14px;
}

.section-title {
  margin: 25px 0 15px;
  font-size: 23px;
}

.forecast {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
  gap: 12px;
}

.day {
  background: rgba(255,255,255,0.12);
  border-radius: 16px;
  padding: 18px 10px;
  text-align: center;
}

.day strong {
  display: block;
  margin-bottom: 10px;
}

.icon {
  font-size: 35px;
  margin: 8px 0;
}

.map-buttons {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
}

.map-buttons button {
  padding: 18px;
  border: none;
  border-radius: 15px;
  background: rgba(255,255,255,0.13);
  color: white;
  cursor: pointer;
  font-size: 16px;
}

.map-buttons button:hover {
  background: rgba(255,255,255,0.22);
}

footer {
  text-align: center;
  padding: 30px;
  opacity: 0.65;
}

@media(max-width:650px) {
  .details,
  .map-buttons {
    grid-template-columns: 1fr;
  }

  .temperature {
    font-size: 55px;
  }
}
</style>
</head>

<body>

<header>
  <h1>🇬🇷 Greece Weather</h1>
  <p>Πρόγνωση καιρού για όλη την Ελλάδα</p>
</header>

<div class="container">

  <div class="search">
    <input id="cityInput" type="text" placeholder="Γράψε πόλη...">
    <button onclick="searchCity()">Αναζήτηση</button>
  </div>

  <section class="current">
    <div class="city" id="city">Θεσσαλονίκη</div>
    <div class="temperature" id="temperature">--°</div>
    <div class="condition" id="condition">Φόρτωση...</div>

    <div class="details">
      <div class="detail">
        💧 Υγρασία<br>
        <b id="humidity">--%</b>
      </div>

      <div class="detail">
        💨 Άνεμος<br>
        <b id="wind">-- km/h</b>
      </div>

      <div class="detail">
        🌡️ Αίσθηση<br>
        <b id="feels">--°</b>
      </div>
    </div>
  </section>

  <h2 class="section-title">📅 Πρόγνωση 15 ημερών</h2>

  <div class="forecast" id="forecast"></div>

  <h2 class="section-title">🗺️ Καιρικοί χάρτες</h2>

  <div class="map-buttons">
    <button onclick="showMap('temperature')">
      🌡️ Θερμοκρασία
    </button>

    <button onclick="showMap('rain')">
      🌧️ Βροχή / Χιόνι
    </button>

    <button onclick="showMap('wind')">
      💨 Άνεμοι
    </button>
  </div>

  <div id="mapArea" style="
    margin-top:20px;
    background:rgba(255,255,255,0.1);
    padding:25px;
    border-radius:20px;
    text-align:center;
  ">
    🗺️ Επίλεξε έναν χάρτη
  </div>

</div>

<footer>
  Greece Weather © 2026
</footer>

<script>

let latitude = 40.6401;
let longitude = 22.9444;
let currentCity = "Θεσσαλονίκη";

async function getWeather() {

  try {

    const url =
      `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}` +
      `&current=temperature_2m,relative_humidity_2m,apparent_temperature,wind_speed_10m,weather_code` +
      `&daily=weather_code,temperature_2m_max,temperature_2m_min` +
      `&forecast_days=15&timezone=auto`;

    const response = await fetch(url);
    const data = await response.json();

    document.getElementById("temperature").textContent =
      Math.round(data.current.temperature_2m) + "°C";

    document.getElementById("humidity").textContent =
      data.current.relative_humidity_2m + "%";

    document.getElementById("wind").textContent =
      Math.round(data.current.wind_speed_10m) + " km/h";

    document.getElementById("feels").textContent =
      Math.round(data.current.apparent_temperature) + "°C";

    document.getElementById("condition").textContent =
      weatherText(data.current.weather_code);

    const forecast = document.getElementById("forecast");
    forecast.innerHTML = "";

    for (let i = 0; i < 15; i++) {

      const date = new Date(data.daily.time[i]);

      const dayName = date.toLocaleDateString("el-GR", {
        weekday: "short"
      });

      const icon = weatherIcon(data.daily.weather_code[i]);

      forecast.innerHTML += `
        <div class="day">
          <strong>${dayName}</strong>
          <div>${date.getDate()}/${date.getMonth()+1}</div>

          <div class="icon">${icon}</div>

          <div>
            <b>${Math.round(data.daily.temperature_2m_max[i])}°</b>
          </div>

          <div style="opacity:.7">
            ${Math.round(data.daily.temperature_2m_min[i])}°
          </div>
        </div>
      `;
    }

  } catch(error) {

    document.getElementById("condition").textContent =
      "Δεν ήταν δυνατή η φόρτωση του καιρού.";

  }
}


function weatherText(code) {

  if (code === 0) return "☀️ Καθαρός ουρανός";
  if (code <= 3) return "⛅ Λίγες νεφώσεις";
  if (code <= 48) return "🌫️ Ομίχλη";
  if (code <= 57) return "🌦️ Ψιλόβροχο";
  if (code <= 67) return "🌧️ Βροχή";
  if (code <= 77) return "❄️ Χιόνι";
  if (code <= 82) return "🌧️ Μπόρες";
  if (code >= 95) return "⛈️ Καταιγίδα";

  return "🌤️ Μεταβλητός καιρός";
}


function weatherIcon(code) {

  if (code === 0) return "☀️";
  if (code <= 3) return "⛅";
  if (code <= 48) return "🌫️";
  if (code <= 67) return "🌧️";
  if (code <= 77) return "❄️";
  if (code <= 82) return "🌦️";
  if (code >= 95) return "⛈️";

  return "🌤️";
}


async function searchCity() {

  const input =
    document.getElementById("cityInput").value.trim();

  if (!input) return;

  try {

    const geoUrl =
      `https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(input)}` +
      `&count=1&language=el&format=json`;

    const response = await fetch(geoUrl);
    const data = await response.json();

    if (!data.results || data.results.length === 0) {
      alert("Δεν βρέθηκε η πόλη.");
      return;
    }

    const place = data.results[0];

    latitude = place.latitude;
    longitude = place.longitude;
    currentCity = place.name;

    document.getElementById("city").textContent =
      currentCity;

    getWeather();

  } catch(error) {

    alert("Κάτι πήγε στραβά.");

  }
}


function showMap(type) {

  const mapArea = document.getElementById("mapArea");

  if (type === "temperature") {

    mapArea.innerHTML = `
      <h2>🌡️ Χάρτης Θερμοκρασίας Ελλάδας</h2>
      <p style="margin-top:10px">
        Χάρτης θερμοκρασίας 850 hPa
      </p>
    `;

  }

  if (type === "rain") {

    mapArea.innerHTML = `
      <h2>🌧️ Χάρτης Βροχής / Χιονιού</h2>
      <p style="margin-top:10px">
        Προβλεπόμενα φαινόμενα στην Ελλάδα
      </p>
    `;

  }

  if (type === "wind") {

    mapArea.innerHTML = `
      <h2>💨 Χάρτης Ανέμων Ελλάδας</h2>
      <p style="margin-top:10px">
        Πρόγνωση ανέμων
      </p>
    `;

  }

}


getWeather();

</script>

</body>
</html>
