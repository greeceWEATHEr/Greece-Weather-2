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
    background: #06284a;
    color: white;
    font-family: Arial, Helvetica, sans-serif;
}

.container {
    width: 100%;
    max-width: 1050px;
    margin: auto;
    padding: 15px;
}

/* ================= HEADER ================= */

.header {
    text-align: center;
    padding: 15px 10px;
    border-bottom: 1px solid #66809c;
    margin-bottom: 15px;
}

.header h1 {
    margin: 0 0 7px;
    font-size: 25px;
}

.header p {
    margin: 0;
    color: #cbd7e3;
    font-size: 13px;
}


/* ================= SEARCH ================= */

.search {
    display: flex;
    gap: 8px;
    margin-bottom: 8px;
}

.search input {
    flex: 1;
    height: 45px;
    border: none;
    border-radius: 10px;
    padding: 0 15px;
    font-size: 15px;
    outline: none;
}

.search button {
    height: 45px;
    border: none;
    border-radius: 10px;
    padding: 0 18px;
    background: white;
    color: #173b5d;
    font-weight: bold;
    cursor: pointer;
}


/* ================= SEARCH RESULTS ================= */

.search-results {
    display: none;
    background: #244b6c;
    border-radius: 10px;
    margin-bottom: 12px;
    overflow: hidden;
}

.location-result {
    padding: 11px 14px;
    border-bottom: 1px solid rgba(255,255,255,.12);
    cursor: pointer;
}

.location-result:last-child {
    border-bottom: none;
}

.location-result:hover {
    background: #315b7e;
}

.location-name {
    font-weight: bold;
    font-size: 14px;
}

.location-details {
    color: #c9d7e3;
    font-size: 11px;
    margin-top: 3px;
}


/* ================= CURRENT WEATHER ================= */

.current {
    background: #315575;
    border-radius: 12px;
    padding: 16px;
    text-align: center;
    box-shadow: 0 2px 8px rgba(0,0,0,.15);
}

.location-title {
    font-size: 20px;
    font-weight: bold;
}

.country {
    color: #cad7e2;
    font-size: 12px;
    margin-top: 4px;
}

.current-icon {
    font-size: 54px;
    margin-top: 10px;
}

.current-temp {
    font-size: 43px;
    font-weight: 300;
    margin-top: 3px;
}

.current-condition {
    font-size: 14px;
    margin: 5px 0 16px;
}

.current-info {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
}

.info {
    background: #416685;
    border-radius: 8px;
    padding: 10px 5px;
    font-size: 11px;
}

.info strong {
    display: block;
    margin-top: 5px;
    font-size: 12px;
}


/* ================= SECTION ================= */

.section-title {
    margin: 21px 0 10px;
    font-size: 17px;
    font-weight: bold;
}


/* ================= 15 DAY ================= */

.forecast-grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 7px;
}

.day {
    background: #315575;
    border-radius: 9px;
    padding: 10px 5px;
    text-align: center;
    min-height: 155px;
    cursor: pointer;
    border: 2px solid transparent;
    transition: .15s;
}

.day:hover {
    background: #3b6384;
}

.day.selected {
    border-color: white;
}

.day-name {
    font-size: 12px;
    font-weight: bold;
}

.date {
    font-size: 10px;
    color: #d0dce7;
    margin-top: 3px;
}

.day-icon {
    font-size: 29px;
    margin: 12px 0 5px;
}

.max {
    font-size: 16px;
    font-weight: bold;
}

.min {
    font-size: 12px;
    color: #d1dce7;
    margin-top: 4px;
}

.rain {
    font-size: 10px;
    margin-top: 9px;
    color: #dbe6ef;
}


/* ================= SELECTED DAY ================= */

.selected-day-title {
    background: #315575;
    border-radius: 10px;
    padding: 13px;
    margin-bottom: 7px;
    font-size: 14px;
    font-weight: bold;
}


/* ================= HOURLY ================= */

.hourly {
    display: flex;
    flex-direction: column;
    gap: 5px;
}

.hour {
    background: #315575;
    border-radius: 8px;
    display: grid;
    grid-template-columns: 65px 45px 1fr 80px 105px;
    align-items: center;
    min-height: 52px;
    padding: 5px 10px;
    font-size: 11px;
}

.hour-time {
    font-weight: bold;
}

.hour-icon {
    font-size: 21px;
}

.hour-condition {
    color: #d3dee8;
}

.hour-rain {
    text-align: center;
}

.wind {
    text-align: right;
}


/* ================= LOADING ================= */

.loading {
    background: #315575;
    border-radius: 10px;
    padding: 20px;
    text-align: center;
    color: #d6e1eb;
}

.error {
    background: #6b3c3c;
    border-radius: 10px;
    padding: 15px;
    text-align: center;
}


/* ================= MOBILE ================= */

@media (max-width: 700px) {

    .forecast-grid {
        grid-template-columns: repeat(3, 1fr);
    }

    .current-info {
        grid-template-columns: repeat(2, 1fr);
    }

    .hour {
        grid-template-columns: 48px 38px 1fr 65px;
    }

    .wind {
        display: none;
    }
}

@media (max-width: 430px) {

    .container {
        padding: 10px;
    }

    .header h1 {
        font-size: 22px;
    }

    .forecast-grid {
        grid-template-columns: repeat(3, 1fr);
    }

    .day {
        min-height: 140px;
    }

    .hour {
        grid-template-columns: 43px 32px 1fr 55px;
        font-size: 10px;
    }

    .current-temp {
        font-size: 39px;
    }
}

</style>
</head>


<body>

<div class="container">


<!-- ================= HEADER ================= -->

<div class="header">

    <h1>🌊 Greece Weather</h1>

    <p>Πρόγνωση καιρού για όλο τον κόσμο</p>

</div>


<!-- ================= SEARCH ================= -->

<div class="search">

    <input
        id="searchInput"
        type="text"
        placeholder="Αναζήτηση πόλης ή περιοχής..."
        autocomplete="off"
    >

    <button onclick="searchLocation()">
        Αναζήτηση
    </button>

</div>


<div id="searchResults" class="search-results"></div>


<!-- ================= CURRENT ================= -->

<div id="currentWeather" class="current">

    <div class="loading">
        Φόρτωση καιρού...
    </div>

</div>


<!-- ================= 15 DAYS ================= -->

<div class="section-title">
    📅 Πρόγνωση 15 ημερών
</div>

<div id="forecast" class="forecast-grid">

    <div class="loading">
        Φόρτωση πρόγνωσης...
    </div>

</div>


<!-- ================= SELECTED DAY ================= -->

<div class="section-title">
    Αναλυτική πρόγνωση
</div>

<div id="selectedDayTitle" class="selected-day-title">
    Επιλέξτε μία ημέρα
</div>

<div id="hourly" class="hourly">

    <div class="loading">
        Επιλέξτε ημέρα για να εμφανιστεί η ωριαία πρόγνωση.
    </div>

</div>


</div>


<script>

/* ============================================================
   GLOBAL STATE
============================================================ */

let currentLocation = {
    name: "Thessaloniki",
    latitude: 40.6401,
    longitude: 22.9444,
    country: "Greece"
};

let weatherData = null;

let selectedDayIndex = 0;


/* ============================================================
   WEATHER CODE
============================================================ */

function weatherInfo(code) {

    const data = {

        0:  ["☀️", "Αίθριος"],
        1:  ["🌤️", "Κυρίως αίθριος"],
        2:  ["⛅", "Μερική συννεφιά"],
        3:  ["☁️", "Συννεφιά"],

        45: ["🌫️", "Ομίχλη"],
        48: ["🌫️", "Πάχνη"],

        51: ["🌦️", "Ψιλόβροχο"],
        53: ["🌦️", "Ψιλόβροχο"],
        55: ["🌦️", "Έντονο ψιλόβροχο"],

        56: ["🌧️", "Παγωμένο ψιλόβροχο"],
        57: ["🌧️", "Παγωμένο ψιλόβροχο"],

        61: ["🌧️", "Ασθενής βροχή"],
        63: ["🌧️", "Βροχή"],
        65: ["🌧️", "Ισχυρή βροχή"],

        66: ["🌧️", "Παγωμένη βροχή"],
        67: ["🌧️", "Ισχυρή παγωμένη βροχή"],

        71: ["🌨️", "Ασθενές χιόνι"],
        73: ["🌨️", "Χιονόπτωση"],
        75: ["❄️", "Ισχυρή χιονόπτωση"],

        77: ["❄️", "Χιονόκοκκοι"],

        80: ["🌦️", "Μπόρες"],
        81: ["🌦️", "Μπόρες"],
        82: ["⛈️", "Ισχυρές μπόρες"],

        85: ["🌨️", "Μπόρες χιονιού"],
        86: ["🌨️", "Ισχυρές μπόρες χιονιού"],

        95: ["⛈️", "Καταιγίδα"],
        96: ["⛈️", "Καταιγίδα με χαλάζι"],
        99: ["⛈️", "Ισχυρή καταιγίδα"]

    };

    return data[code] || ["🌡️", "Άγνωστη κατάσταση"];

}


/* ============================================================
   FORMAT DATE
============================================================ */

function formatDate(dateString) {

    const d = new Date(dateString + "T12:00:00");

    return d.toLocaleDateString("el-GR", {
        day: "numeric",
        month: "numeric"
    });

}


function dayName(dateString) {

    const d = new Date(dateString + "T12:00:00");

    return d.toLocaleDateString("el-GR", {
        weekday: "short"
    });

}


/* ============================================================
   FORMAT WIND DIRECTION
============================================================ */

function windDirection(degrees) {

    if (degrees === null || degrees === undefined) {
        return "-";
    }

    const directions = [
        "Β",
        "ΒΑ",
        "Α",
        "ΝΑ",
        "Ν",
        "ΝΔ",
        "Δ",
        "ΒΔ"
    ];

    const index = Math.round(degrees / 45) % 8;

    return directions[index];

}


/* ============================================================
   SEARCH GLOBAL LOCATION
============================================================ */

async function searchLocation() {

    const input =
        document.getElementById("searchInput").value.trim();

    if (input.length < 2) {
        return;
    }

    const resultsBox =
        document.getElementById("searchResults");

    resultsBox.style.display = "block";

    resultsBox.innerHTML =
        `<div class="location-result">
            Αναζήτηση...
        </div>`;

    try {

        const url =
            "https://geocoding-api.open-meteo.com/v1/search" +
            "?name=" + encodeURIComponent(input) +
            "&count=10" +
            "&language=el" +
            "&format=json";

        const response = await fetch(url);

        if (!response.ok) {
            throw new Error("Geocoding error");
        }

        const data = await response.json();

        resultsBox.innerHTML = "";

        if (!data.results || data.results.length === 0) {

            resultsBox.innerHTML =
                `<div class="location-result">
                    Δεν βρέθηκε περιοχή.
                </div>`;

            return;
        }


        data.results.forEach(location => {

            const item =
                document.createElement("div");

            item.className = "location-result";

            const name =
                location.name || "";

            const country =
                location.country || "";

            const admin =
                location.admin1 || "";

            item.innerHTML = `

                <div class="location-name">
                    ${name}
                </div>

                <div class="location-details">
                    ${admin ? admin + ", " : ""}
                    ${country}
                </div>

            `;


            item.onclick = () => {

                currentLocation = {

                    name:
                        location.name,

                    latitude:
                        location.latitude,

                    longitude:
                        location.longitude,

                    country:
                        location.country || ""

                };

                document.getElementById("searchInput")
                    .value = location.name;

                resultsBox.style.display = "none";

                loadWeather();

            };


            resultsBox.appendChild(item);

        });

    }

    catch (error) {

        resultsBox.innerHTML =
            `<div class="location-result">
                Δεν ήταν δυνατή η αναζήτηση.
            </div>`;

        console.error(error);

    }

}


/* ============================================================
   ENTER KEY SEARCH
============================================================ */

document
    .getElementById("searchInput")
    .addEventListener("keydown", function(event) {

        if (event.key === "Enter") {

            searchLocation();

        }

    });


/* ============================================================
   LOAD REAL WEATHER
============================================================ */

async function loadWeather() {

    document.getElementById("currentWeather").innerHTML =
        `<div class="loading">Φόρτωση καιρού...</div>`;

    document.getElementById("forecast").innerHTML =
        `<div class="loading">Φόρτωση πρόγνωσης...</div>`;

    try {

        const variables = [

            "temperature_2m",
            "relative_humidity_2m",
            "apparent_temperature",
            "precipitation_probability",
            "precipitation",
            "weather_code",
            "wind_speed_10m",
            "wind_direction_10m",
            "wind_gusts_10m"

        ].join(",");


        const dailyVariables = [

            "weather_code",
            "temperature_2m_max",
            "temperature_2m_min",
            "apparent_temperature_max",
            "apparent_temperature_min",
            "precipitation_sum",
            "precipitation_probability_max",
            "wind_speed_10m_max",
            "wind_gusts_10m_max",
            "wind_direction_10m_dominant",
            "sunrise",
            "sunset"

        ].join(",");


        const url =

            "https://api.open-meteo.com/v1/forecast" +

            "?latitude=" +
            encodeURIComponent(currentLocation.latitude) +

            "&longitude=" +
            encodeURIComponent(currentLocation.longitude) +

            "&hourly=" +
            encodeURIComponent(variables) +

            "&daily=" +
            encodeURIComponent(dailyVariables) +

            "&forecast_days=16" +

            "&timezone=auto" +

            "&temperature_unit=celsius" +

            "&wind_speed_unit=kmh" +

            "&precipitation_unit=mm" +

            "&_=" + Date.now();


        const response = await fetch(url, {
            cache: "no-store"
        });


        if (!response.ok) {
            throw new Error("Weather API error");
        }


        weatherData = await response.json();


        renderCurrent();

        renderForecast();

        selectDay(selectedDayIndex);

    }

    catch (error) {

        console.error(error);

        document.getElementById("currentWeather").innerHTML =
            `<div class="error">
                Δεν ήταν δυνατή η φόρτωση των δεδομένων καιρού.
            </div>`;

    }

}


/* ============================================================
   CURRENT WEATHER
============================================================ */

function renderCurrent() {

    const h = weatherData.hourly;

    const currentHour = 0;

    const temp =
        Math.round(h.temperature_2m[currentHour]);

    const feels =
        Math.round(h.apparent_temperature[currentHour]);

    const humidity =
        Math.round(h.relative_humidity_2m[currentHour]);

    const wind =
        Math.round(h.wind_speed_10m[currentHour]);

    const gust =
        Math.round(h.wind_gusts_10m[currentHour]);

    const direction =
        windDirection(h.wind_direction_10m[currentHour]);

    const code =
        h.weather_code[currentHour];

    const info =
        weatherInfo(code);


    document.getElementById("currentWeather").innerHTML = `

        <div class="location-title">
            ${currentLocation.name}
        </div>

        <div class="country">
            ${currentLocation.country}
        </div>

        <div class="current-icon">
            ${info[0]}
        </div>

        <div class="current-temp">
            ${temp}°C
        </div>

        <div class="current-condition">
            ${info[1]}
        </div>

        <div class="current-info">

            <div class="info">
                💧 Υγρασία
                <strong>${humidity}%</strong>
            </div>

            <div class="info">
                🌡️ Αίσθηση
                <strong>${feels}°C</strong>
            </div>

            <div class="info">
                💨 Άνεμος
                <strong>${wind} km/h ${direction}</strong>
            </div>

            <div class="info">
                💨 Ριπές
                <strong>${gust} km/h</strong>
            </div>

        </div>

    `;

}


/* ============================================================
   15 DAY FORECAST
============================================================ */

function renderForecast() {

    const box =
        document.getElementById("forecast");

    box.innerHTML = "";

    const d =
        weatherData.daily;


    /* Εμφάνιση 15 ημερών */
    for (let i = 0; i < 15; i++) {

        const info =
            weatherInfo(d.weather_code[i]);


        const card =
            document.createElement("div");

        card.className = "day";

        if (i === selectedDayIndex) {
            card.classList.add("selected");
        }


        card.innerHTML = `

            <div class="day-name">
                ${dayName(d.time[i])}
            </div>

            <div class="date">
                ${formatDate(d.time[i])}
            </div>

            <div class="day-icon">
                ${info[0]}
            </div>

            <div class="max">
                ${Math.round(d.temperature_2m_max[i])}°
            </div>

            <div class="min">
                ${Math.round(d.temperature_2m_min[i])}°
            </div>

            <div class="rain">
                💧 ${d.precipitation_probability_max[i] ?? 0}%
            </div>

        `;


        card.onclick = () => {

            selectDay(i);

        };


        box.appendChild(card);

    }

}


/* ============================================================
   SELECT DAY
============================================================ */

function selectDay(index) {

    selectedDayIndex = index;

    renderForecast();

    renderHourlyDay(index);

}


/* ============================================================
   HOURLY FORECAST FOR SELECTED DAY
============================================================ */

function renderHourlyDay(dayIndex) {

    const hourly =
        weatherData.hourly;

    const daily =
        weatherData.daily;


    const selectedDate =
        daily.time[dayIndex];


    document.getElementById("selectedDayTitle")
        .textContent =
        "📅 " +
        dayName(selectedDate) +
        " " +
        formatDate(selectedDate) +
        " — Αναλυτική πρόγνωση";


    const box =
        document.getElementById("hourly");

    box.innerHTML = "";


    for (let i = 0;
         i < hourly.time.length;
         i++) {


        const time =
            hourly.time[i];


        if (!time.startsWith(selectedDate)) {
            continue;
        }


        const dateObject =
            new Date(time);


        const hour =
            dateObject
                .getHours()
                .toString()
                .padStart(2, "0");


        const minute =
            dateObject
                .getMinutes()
                .toString()
                .padStart(2, "0");


        const info =
            weatherInfo(hourly.weather_code[i]);


        const temp =
            Math.round(
                hourly.temperature_2m[i]
            );


        const rain =
            hourly.precipitation_probability[i] ?? 0;


        const wind =
            Math.round(
                hourly.wind_speed_10m[i]
            );


        const direction =
            windDirection(
                hourly.wind_direction_10m[i]
            );


        const gust =
            Math.round(
                hourly.wind_gusts_10m[i]
            );


        const row =
            document.createElement("div");

        row.className = "hour";


        row.innerHTML = `

            <div class="hour-time">
                ${hour}:${minute}
            </div>

            <div class="hour-icon">
                ${info[0]}
            </div>

            <div class="hour-condition">
                ${temp}°C<br>
                ${info[1]}
            </div>

            <div class="hour-rain">
                💧 ${rain}%
            </div>

            <div class="wind">
                💨 ${wind} km/h<br>
                ${direction} · ${gust} km/h
            </div>

        `;


        box.appendChild(row);

    }

}


/* ============================================================
   AUTOMATIC DATA UPDATE
============================================================ */

/*
   Κάθε 5 λεπτά η σελίδα ζητά ξανά τα τελευταία διαθέσιμα
   δεδομένα από το API.

   Δεν εμφανίζεται κανένα μήνυμα στον επισκέπτη.
*/

setInterval(() => {

    loadWeather();

}, 5 * 60 * 1000);


/* ============================================================
   INITIAL LOAD
============================================================ */

loadWeather();

</script>

</body>
</html>
