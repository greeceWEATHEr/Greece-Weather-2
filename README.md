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
<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<style>
    * {
        box-sizing: border-box;
    }

    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background: #0b2949;
        color: white;
    }

    .container {
        max-width: 1100px;
        margin: auto;
        padding: 25px 20px 40px;
    }

    .header {
        text-align: center;
        background: #081f38;
        padding: 35px 15px;
        border-radius: 4px;
        margin-bottom: 25px;
    }

    .header h1 {
        margin: 0;
        font-size: 32px;
    }

    .header p {
        margin-top: 18px;
        font-size: 17px;
        color: #cbd5df;
    }

    .search {
        display: flex;
        gap: 10px;
        margin-bottom: 25px;
    }

    .search input {
        flex: 1;
        padding: 17px;
        border: none;
        border-radius: 14px;
        font-size: 16px;
    }

    .search button {
        padding: 0 25px;
        border: none;
        border-radius: 14px;
        font-weight: bold;
        font-size: 16px;
        cursor: pointer;
    }

    .current {
        background: #304b69;
        border-radius: 20px;
        padding: 28px 20px;
        text-align: center;
        margin-bottom: 25px;
    }

    .current h2 {
        margin: 0 0 25px;
        font-size: 25px;
    }

    .current-temp {
        font-size: 62px;
        margin-bottom: 10px;
    }

    .current-desc {
        font-size: 18px;
        margin-bottom: 25px;
    }

    .current-info {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 12px;
    }

    .info-box {
        background: #49637f;
        border-radius: 14px;
        padding: 15px 5px;
    }

    .info-box span {
        display: block;
        font-size: 14px;
        margin-bottom: 7px;
    }

    .info-box strong {
        font-size: 15px;
    }

    .title {
        font-size: 25px;
        font-weight: bold;
        margin: 25px 0 10px;
        border-bottom: 1px solid #8ea0b2;
        padding-bottom: 10px;
    }

    .forecast {
        display: grid;
        grid-template-columns: repeat(6, 1fr);
        gap: 12px;
    }

    .card {
        background: #304b69;
        border-radius: 17px;
        min-height: 205px;
        padding: 18px 8px 13px;
        text-align: center;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .day {
        font-size: 15px;
        font-weight: bold;
        margin-bottom: 9px;
    }

    .date {
        font-size: 14px;
        color: #e0e7ee;
        margin-bottom: 15px;
    }

    .icon {
        font-size: 36px;
        height: 45px;
        margin-bottom: 9px;
    }

    .max {
        font-size: 16px;
        font-weight: bold;
        margin-top: 4px;
    }

    .min {
        font-size: 14px;
        color: #cbd5df;
        margin-top: 6px;
    }

    /* ΥΕΤΟΣ */
    .precipitation {
        margin-top: auto;
        padding-top: 11px;
        font-size: 13px;
        font-weight: bold;
        color: #dcecff;
    }

    .precipitation .amount {
        display: block;
        margin-top: 4px;
        font-size: 14px;
    }

    .loading {
        text-align: center;
        padding: 30px;
        font-size: 18px;
    }

    .error {
        text-align: center;
        color: #ffd0d0;
        padding: 20px;
    }

    @media (max-width: 900px) {
        .forecast {
            grid-template-columns: repeat(4, 1fr);
        }
    }

    @media (max-width: 600px) {
        .container {
            padding: 15px 10px 30px;
        }

        .forecast {
            grid-template-columns: repeat(3, 1fr);
        }

        .current-info {
            grid-template-columns: 1fr;
        }

        .header h1 {
            font-size: 27px;
        }

        .search button {
            padding: 0 16px;
        }
    }
</style>
</head>

<body>

<div class="container">

    <div class="header">
        <h1>🇬🇷 Greece Weather</h1>
        <p>Πρόγνωση καιρού για όλη την Ελλάδα</p>
    </div>

    <div class="search">
        <input
            id="cityInput"
            type="text"
            placeholder="Γράψε πόλη..."
            value="Θεσσαλονίκη"
        >
        <button onclick="searchCity()">Αναζήτηση</button>
    </div>

    <div id="currentWeather" class="current">
        <div class="loading">Φόρτωση καιρού...</div>
    </div>

    <div class="title">📅 Πρόγνωση 15 ημερών</div>

    <div id="forecast" class="forecast">
        <div class="loading">Φόρτωση πρόγνωσης...</div>
    </div>

</div>

<script>

/* =========================================================
   ΡΥΘΜΙΣΕΙΣ
   ========================================================= */

let latitude = 40.6401;
let longitude = 22.9444;
let cityName = "Θεσσαλονίκη";


/* =========================================================
   ΑΝΑΖΗΤΗΣΗ ΠΟΛΗΣ
   ========================================================= */

async function searchCity() {

    const input = document.getElementById("cityInput").value.trim();

    if (!input) return;

    try {

        const url =
            "https://geocoding-api.open-meteo.com/v1/search" +
            "?name=" + encodeURIComponent(input) +
            "&count=1" +
            "&language=el" +
            "&format=json";

        const response = await fetch(url);
        const data = await response.json();

        if (!data.results || data.results.length === 0) {
            alert("Δεν βρέθηκε η πόλη.");
            return;
        }

        const place = data.results[0];

        latitude = place.latitude;
        longitude = place.longitude;
        cityName = place.name;

        loadWeather();

    } catch (error) {

        console.error(error);
        alert("Παρουσιάστηκε πρόβλημα στην αναζήτηση.");

    }
}


/* =========================================================
   WEATHER CODE → ΕΙΚΟΝΑ / ΠΕΡΙΓΡΑΦΗ
   ========================================================= */

function weatherInfo(code) {

    if (code === 0)
        return ["☀️", "Καθαρός"];

    if (code === 1)
        return ["🌤️", "Κυρίως αίθριος"];

    if (code === 2)
        return ["⛅", "Μερική συννεφιά"];

    if (code === 3)
        return ["☁️", "Συννεφιά"];

    if ([45, 48].includes(code))
        return ["🌫️", "Ομίχλη"];

    if ([51, 53, 55].includes(code))
        return ["🌦️", "Ψιλή βροχή"];

    if ([56, 57].includes(code))
        return ["🌧️", "Παγωμένη ψιλή βροχή"];

    if ([61, 63, 65].includes(code))
        return ["🌧️", "Βροχή"];

    if ([66, 67].includes(code))
        return ["🌧️", "Παγωμένη βροχή"];

    if ([71, 73, 75, 77].includes(code))
        return ["❄️", "Χιόνι"];

    if ([80, 81, 82].includes(code))
        return ["🌧️", "Μπόρες"];

    if ([85, 86].includes(code))
        return ["🌨️", "Χιονομπόρες"];

    if ([95].includes(code))
        return ["⛈️", "Καταιγίδα"];

    if ([96, 99].includes(code))
        return ["⛈️", "Καταιγίδα με χαλάζι"];

    return ["🌤️", "Μεταβλητός"];
}


/* =========================================================
   ΟΝΟΜΑ ΗΜΕΡΑΣ
   ========================================================= */

function getDayName(dateString) {

    const date = new Date(dateString + "T12:00:00");

    const days = [
        "Κυρ",
        "Δευ",
        "Τρί",
        "Τετ",
        "Πέμ",
        "Παρ",
        "Σάβ"
    ];

    return days[date.getDay()];
}


/* =========================================================
   ΗΜΕΡΟΜΗΝΙΑ
   ========================================================= */

function getDateText(dateString) {

    const date = new Date(dateString + "T12:00:00");

    return (
        String(date.getDate()).padStart(2, "0") +
        "/" +
        String(date.getMonth() + 1).padStart(2, "0")
    );
}


/* =========================================================
   ΥΕΤΟΣ
   =========================================================

   Βροχή → mm
   Χιόνι → cm

   Το Open-Meteo επιστρέφει snowfall_sum
   σε cm και precipitation_sum / rain_sum σε mm.
   ========================================================= */

function getPrecipitationText(
    precipitation,
    rain,
    snowfall
) {

    precipitation = Number(precipitation || 0);
    rain = Number(rain || 0);
    snowfall = Number(snowfall || 0);


    /* Αν προβλέπεται χιόνι */
    if (snowfall > 0) {

        return `
            ❄️ Χιόνι
            <span class="amount">
                ${snowfall.toFixed(1)} cm
            </span>
        `;
    }


    /* Αν προβλέπεται βροχή */
    if (rain > 0) {

        return `
            💧 Βροχή
            <span class="amount">
                ${rain.toFixed(1)} mm
            </span>
        `;
    }


    /* Άλλος υετός */
    if (precipitation > 0) {

        return `
            💧 Υετός
            <span class="amount">
                ${precipitation.toFixed(1)} mm
            </span>
        `;
    }


    /* Καθόλου υετός */

    return `
        💧 Υετός
        <span class="amount">
            0 mm
        </span>
    `;
}


/* =========================================================
   ΦΟΡΤΩΣΗ ΚΑΙΡΟΥ
   ========================================================= */

async function loadWeather() {

    const currentBox =
        document.getElementById("currentWeather");

    const forecastBox =
        document.getElementById("forecast");


    currentBox.innerHTML =
        '<div class="loading">Φόρτωση καιρού...</div>';

    forecastBox.innerHTML =
        '<div class="loading">Φόρτωση πρόγνωσης...</div>';


    try {

        const url =
            "https://api.open-meteo.com/v1/forecast" +

            "?latitude=" + latitude +
            "&longitude=" + longitude +

            "&current=" +
            "temperature_2m," +
            "relative_humidity_2m," +
            "apparent_temperature," +
            "wind_speed_10m," +
            "weather_code" +

            "&daily=" +
            "weather_code," +
            "temperature_2m_max," +
            "temperature_2m_min," +
            "precipitation_sum," +
            "rain_sum," +
            "snowfall_sum" +

            "&timezone=Europe%2FAthens" +

            "&forecast_days=15";


        const response = await fetch(url);

        if (!response.ok) {
            throw new Error("Weather API error");
        }

        const data = await response.json();


        /* =================================================
           ΤΡΕΧΩΝ ΚΑΙΡΟΣ
           ================================================= */

        const current = data.current;

        const currentInfo =
            weatherInfo(current.weather_code);


        currentBox.innerHTML = `

            <h2>${cityName}</h2>

            <div class="current-temp">
                ${Math.round(current.temperature_2m)}°C
            </div>

            <div class="current-desc">
                ${currentInfo[0]}
                ${currentInfo[1]}
            </div>

            <div class="current-info">

                <div class="info-box">
                    <span>💧 Υγρασία</span>
                    <strong>
                        ${current.relative_humidity_2m}%
                    </strong>
                </div>

                <div class="info-box">
                    <span>💨 Άνεμος</span>
                    <strong>
                        ${Math.round(current.wind_speed_10m)} km/h
                    </strong>
                </div>

                <div class="info-box">
                    <span>🌡️ Αίσθηση</span>
                    <strong>
                        ${Math.round(current.apparent_temperature)}°C
                    </strong>
                </div>

            </div>
        `;


        /* =================================================
           15ΗΜΕΡΗ ΠΡΟΓΝΩΣΗ
           ================================================= */

        let html = "";


        for (let i = 0; i < data.daily.time.length; i++) {

            const date =
                data.daily.time[i];

            const code =
                data.daily.weather_code[i];

            const max =
                data.daily.temperature_2m_max[i];

            const min =
                data.daily.temperature_2m_min[i];

            const precipitation =
                data.daily.precipitation_sum[i];

            const rain =
                data.daily.rain_sum[i];

            const snowfall =
                data.daily.snowfall_sum[i];


            const info =
                weatherInfo(code);


            const precipitationText =
                getPrecipitationText(
                    precipitation,
                    rain,
                    snowfall
                );


            html += `

                <div class="card">

                    <div class="day">
                        ${getDayName(date)}
                    </div>

                    <div class="date">
                        ${getDateText(date)}
                    </div>

                    <div class="icon">
                        ${info[0]}
                    </div>

                    <div class="max">
                        ${Math.round(max)}°
                    </div>

                    <div class="min">
                        ${Math.round(min)}°
                    </div>

                    <div class="precipitation">
                        ${precipitationText}
                    </div>

                </div>

            `;
        }


        forecastBox.innerHTML = html;


    } catch (error) {

        console.error(error);

        currentBox.innerHTML = `
            <div class="error">
                Δεν ήταν δυνατή η φόρτωση του καιρού.
            </div>
        `;

        forecastBox.innerHTML = `
            <div class="error">
                Ελέγξτε τη σύνδεσή σας και δοκιμάστε ξανά.
            </div>
        `;
    }
}


/* =========================================================
   ΑΡΧΙΚΗ ΦΟΡΤΩΣΗ
   ========================================================= */

loadWeather();

</script>

</body>
</html>
