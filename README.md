<!DOCTYPE html>
<html lang="el">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<style>

/* =========================================================
   ΒΑΣΙΚΑ
========================================================= */

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


/* =========================================================
   HEADER
========================================================= */

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


/* =========================================================
   ΑΝΑΖΗΤΗΣΗ
========================================================= */

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

.search button:hover {
    background: #e9eef3;
}


/* =========================================================
   ΑΠΟΤΕΛΕΣΜΑΤΑ ΑΝΑΖΗΤΗΣΗΣ
========================================================= */

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


/* =========================================================
   ΤΡΕΧΩΝ ΚΑΙΡΟΣ
========================================================= */

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
    line-height: 1.1;
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
    grid-template-columns: repeat(3, 1fr);
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


/* =========================================================
   ΤΙΤΛΟΙ
========================================================= */

.section-title {
    margin: 21px 0 10px;
    font-size: 17px;
    font-weight: bold;
}


/* =========================================================
   15 ΗΜΕΡΕΣ
========================================================= */

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
    line-height: 1.1;
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


/* =========================================================
   ΕΠΙΛΕΓΜΕΝΗ ΗΜΕΡΑ
========================================================= */

.selected-day-title {
    background: #315575;
    border-radius: 10px;
    padding: 13px;
    margin-bottom: 7px;
    font-size: 14px;
    font-weight: bold;
}


/* =========================================================
   ΩΡΙΑΙΑ
========================================================= */

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
    line-height: 1;
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


/* =========================================================
   ΦΕΓΓΑΡΙ / ΝΥΧΤΕΡΙΝΑ ΕΙΚΟΝΙΔΙΑ
========================================================= */

.moon-icon {
    filter: grayscale(1);
    opacity: .82;
    display: inline-block;
}

.night-cloud-icon {
    filter: grayscale(1);
    opacity: .82;
    display: inline-block;
}

.night-cloud-only {
    filter: grayscale(1);
    opacity: .82;
    display: inline-block;
}


/* =========================================================
   LOADING
========================================================= */

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


/* =========================================================
   MOBILE
========================================================= */

@media (max-width: 700px) {

    .forecast-grid {
        grid-template-columns: repeat(3, 1fr);
    }

    .current-info {
        grid-template-columns: repeat(3, 1fr);
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


<!-- =====================================================
     HEADER
===================================================== -->

<div class="header">

    <h1>🌊 Greece Weather</h1>

    <p>Πρόγνωση καιρού για όλο τον κόσμο</p>

</div>


<!-- =====================================================
     ΑΝΑΖΗΤΗΣΗ
===================================================== -->

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


<!-- =====================================================
     ΤΡΕΧΩΝ ΚΑΙΡΟΣ
===================================================== -->

<div id="currentWeather" class="current">

    <div class="loading">
        Φόρτωση καιρού...
    </div>

</div>


<!-- =====================================================
     15ΗΜΕΡΟ
===================================================== -->

<div class="section-title">
    📅 Πρόγνωση 15 ημερών
</div>

<div id="forecast" class="forecast-grid">

    <div class="loading">
        Φόρτωση πρόγνωσης...
    </div>

</div>


<!-- =====================================================
     ΑΝΑΛΥΤΙΚΗ ΠΡΟΓΝΩΣΗ
===================================================== -->

<div class="section-title">
    Αναλυτική πρόγνωση
</div>

<div id="selectedDayTitle" class="selected-day-title">
    Φόρτωση...
</div>

<div id="hourly" class="hourly">

    <div class="loading">
        Φόρτωση...
    </div>

</div>


</div>


<script>

/* =========================================================
   ΑΡΧΙΚΗ ΠΕΡΙΟΧΗ
========================================================= */

let currentLocation = {

    name: "Θεσσαλονίκη",

    latitude: 40.6401,

    longitude: 22.9444,

    country: "Ελλάδα"

};


/* =========================================================
   ΔΕΔΟΜΕΝΑ ΚΑΙΡΟΥ
========================================================= */

let weatherData = null;

let selectedDayIndex = 0;


/* =========================================================
   WMO WEATHER CODES
========================================================= */

function weatherInfo(
    code,
    isDay,
    precipitationProbability = 0
) {

    const precip =
        Number(precipitationProbability) >= 30;


    /* =====================================================
       ΝΥΧΤΑ
    ===================================================== */

    if (!isDay) {


        /* ---------------------------------------------
           Κάτω από 30% υετό
        --------------------------------------------- */

        if (!precip) {

            if (code === 0) {

                return [
                    '<span class="moon-icon">🌙</span>',
                    "Καθαρός ουρανός"
                ];

            }


            if (code === 1) {

                return [
                    '<span class="moon-icon">🌙</span>',
                    "Κυρίως καθαρός"
                ];

            }


            if (code === 2) {

                return [
                    '<span class="night-cloud-icon">🌙☁️</span>',
                    "Λίγες νεφώσεις"
                ];

            }


            if (code === 3) {

                return [
                    '<span class="night-cloud-only">☁️</span>',
                    "Συννεφιά"
                ];

            }


            if (code === 45 || code === 48) {

                return [
                    "🌫️",
                    "Ομίχλη"
                ];

            }


            /*
             Όταν ο WMO code υποδεικνύει υετό,
             αλλά η πιθανότητα είναι κάτω από 30%,
             δεν εμφανίζουμε εικονίδιο υετού.
            */

            return [
                '<span class="night-cloud-icon">🌙☁️</span>',
                "Νεφώσεις"
            ];

        }


        /* ---------------------------------------------
           30%+ ΥΕΤΟΣ ΤΗ ΝΥΧΤΑ
        --------------------------------------------- */

        if (
            code === 51 ||
            code === 53 ||
            code === 55
        ) {

            return ["🌧️", "Ψιλόβροχο"];

        }


        if (
            code === 56 ||
            code === 57
        ) {

            return ["🌧️", "Παγωμένο ψιλόβροχο"];

        }


        if (
            code === 61 ||
            code === 63 ||
            code === 65
        ) {

            return ["🌧️", "Βροχή"];

        }


        if (
            code === 66 ||
            code === 67
        ) {

            return ["🌧️", "Παγωμένη βροχή"];

        }


        if (
            code === 71 ||
            code === 73 ||
            code === 75 ||
            code === 77
        ) {

            return ["❄️", "Χιόνι"];

        }


        if (
            code === 80 ||
            code === 81 ||
            code === 82
        ) {

            return ["🌧️", "Μπόρες"];

        }


        if (
            code === 85 ||
            code === 86
        ) {

            return ["🌨️", "Μπόρες χιονιού"];

        }


        if (
            code === 95 ||
            code === 96 ||
            code === 99
        ) {

            return ["⛈️", "Καταιγίδα"];

        }


        return [
            '<span class="night-cloud-icon">🌙☁️</span>',
            "Νεφώσεις"
        ];

    }


    /* =====================================================
       ΗΜΕΡΑ
    ===================================================== */

    if (!precip) {


        if (code === 0) {

            return [
                "☀️",
                "Αίθριος"
            ];

        }


        if (code === 1) {

            return [
                "🌤️",
                "Κυρίως αίθριος"
            ];

        }


        if (code === 2) {

            return [
                "⛅",
                "Λίγες νεφώσεις"
            ];

        }


        if (code === 3) {

            return [
                "☁️",
                "Συννεφιά"
            ];

        }


        if (
            code === 45 ||
            code === 48
        ) {

            return [
                "🌫️",
                "Ομίχλη"
            ];

        }


        /*
         Υετός κάτω από 30%:
         δεν εμφανίζεται εικονίδιο υετού.
        */

        return [
            "⛅",
            "Παροδικές νεφώσεις"
        ];

    }


    /* =====================================================
       30%+ ΥΕΤΟΣ ΗΜΕΡΑΣ
    ===================================================== */

    if (
        code === 51 ||
        code === 53 ||
        code === 55
    ) {

        return [
            "🌦️",
            "Ψιλόβροχο"
        ];

    }


    if (
        code === 56 ||
        code === 57
    ) {

        return [
            "🌧️",
            "Παγωμένο ψιλόβροχο"
        ];

    }


    if (
        code === 61 ||
        code === 63 ||
        code === 65
    ) {

        return [
            "🌧️",
            "Βροχή"
        ];

    }


    if (
        code === 66 ||
        code === 67
    ) {

        return [
            "🌧️",
            "Παγωμένη βροχή"
        ];

    }


    if (
        code === 71 ||
        code === 73 ||
        code === 75 ||
        code === 77
    ) {

        return [
            "❄️",
            "Χιόνι"
        ];

    }


    if (
        code === 80 ||
        code === 81 ||
        code === 82
    ) {

        return [
            "🌦️",
            "Μπόρες"
        ];

    }


    if (
        code === 85 ||
        code === 86
    ) {

        return [
            "🌨️",
            "Μπόρες χιονιού"
        ];

    }


    if (
        code === 95 ||
        code === 96 ||
        code === 99
    ) {

        return [
            "⛈️",
            "Καταιγίδα"
        ];

    }


    return [
        "☀️",
        "Αίθριος"
    ];

}


/* =========================================================
   ΗΜΕΡΑ ΕΒΔΟΜΑΔΑΣ
========================================================= */

function dayName(dateString) {

    const date =
        new Date(dateString + "T12:00:00");

    return date.toLocaleDateString(
        "el-GR",
        {
            weekday: "short"
        }
    );

}


/* =========================================================
   ΗΜΕΡΟΜΗΝΙΑ
========================================================= */

function formatDate(dateString) {

    const date =
        new Date(dateString + "T12:00:00");

    return date.toLocaleDateString(
        "el-GR",
        {
            day: "numeric",
            month: "numeric"
        }
    );

}


/* =========================================================
   ΚΑΤΕΥΘΥΝΣΗ ΑΝΕΜΟΥ
========================================================= */

function windDirection(degrees) {

    if (
        degrees === null ||
        degrees === undefined ||
        Number.isNaN(Number(degrees))
    ) {

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


    const index =
        Math.round(Number(degrees) / 45) % 8;


    return directions[index];

}


/* =========================================================
   ΑΝΑΖΗΤΗΣΗ ΠΕΡΙΟΧΗΣ ΠΑΓΚΟΣΜΙΩΣ
========================================================= */

async function searchLocation() {

    const input =
        document
            .getElementById("searchInput")
            .value
            .trim();


    if (input.length < 2) {

        return;

    }


    const resultsBox =
        document.getElementById(
            "searchResults"
        );


    resultsBox.style.display =
        "block";


    resultsBox.innerHTML = `
        <div class="location-result">
            Αναζήτηση...
        </div>
    `;


    try {

        const url =

            "https://geocoding-api.open-meteo.com/v1/search" +

            "?name=" +
            encodeURIComponent(input) +

            "&count=10" +

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


        resultsBox.innerHTML = "";


        if (
            !data.results ||
            data.results.length === 0
        ) {

            resultsBox.innerHTML = `
                <div class="location-result">
                    Δεν βρέθηκε περιοχή.
                </div>
            `;

            return;

        }


        data.results.forEach(
            location => {

                const item =
                    document.createElement(
                        "div"
                    );


                item.className =
                    "location-result";


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
                        ${
                            admin
                            ? admin + ", "
                            : ""
                        }
                        ${country}
                    </div>

                `;


                item.onclick = () => {


                    currentLocation = {

                        name:
                            location.name,

                        latitude:
                            Number(
                                location.latitude
                            ),

                        longitude:
                            Number(
                                location.longitude
                            ),

                        country:
                            location.country || ""

                    };


                    document
                        .getElementById(
                            "searchInput"
                        )
                        .value =
                        location.name;


                    resultsBox.style.display =
                        "none";


                    selectedDayIndex = 0;


                    loadWeather();

                };


                resultsBox.appendChild(
                    item
                );

            }
        );

    }

    catch (error) {

        console.error(error);


        resultsBox.innerHTML = `
            <div class="location-result">
                Δεν ήταν δυνατή η αναζήτηση.
            </div>
        `;

    }

}


/* =========================================================
   ENTER = ΑΝΑΖΗΤΗΣΗ
========================================================= */

document
    .getElementById("searchInput")
    .addEventListener(
        "keydown",
        function(event) {

            if (
                event.key === "Enter"
            ) {

                searchLocation();

            }

        }
    );


/* =========================================================
   ΦΟΡΤΩΣΗ ΠΡΑΓΜΑΤΙΚΟΥ ΚΑΙΡΟΥ
========================================================= */

async function loadWeather() {


    document
        .getElementById(
            "currentWeather"
        )
        .innerHTML = `
            <div class="loading">
                Φόρτωση καιρού...
            </div>
        `;


    document
        .getElementById(
            "forecast"
        )
        .innerHTML = `
            <div class="loading">
                Φόρτωση πρόγνωσης...
            </div>
        `;


    try {


        const hourlyVariables = [

            "temperature_2m",

            "relative_humidity_2m",

            "apparent_temperature",

            "precipitation_probability",

            "precipitation",

            "rain",

            "showers",

            "snowfall",

            "weather_code",

            "cloud_cover",

            "is_day",

            "wind_speed_10m",

            "wind_direction_10m"

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

            "wind_direction_10m_dominant",

            "sunrise",

            "sunset"

        ].join(",");


        /*
           models=auto:
           Το API επιλέγει/συνδυάζει τα κατάλληλα
           διαθέσιμα μοντέλα για την περιοχή.
        */

        const url =

            "https://api.open-meteo.com/v1/forecast" +

            "?latitude=" +
            encodeURIComponent(
                currentLocation.latitude
            ) +

            "&longitude=" +
            encodeURIComponent(
                currentLocation.longitude
            ) +

            "&hourly=" +
            encodeURIComponent(
                hourlyVariables
            ) +

            "&daily=" +
            encodeURIComponent(
                dailyVariables
            ) +

            "&forecast_days=16" +

            "&timezone=auto" +

            "&temperature_unit=celsius" +

            "&wind_speed_unit=kmh" +

            "&precipitation_unit=mm" +

            "&models=auto" +

            "&cell_selection=land" +

            "&_=" +
            Date.now();


        const response =
            await fetch(
                url,
                {
                    cache: "no-store"
                }
            );


        if (!response.ok) {

            throw new Error(
                "Weather API error"
            );

        }


        weatherData =
            await response.json();


        if (
            !weatherData.hourly ||
            !weatherData.daily
        ) {

            throw new Error(
                "Incomplete weather data"
            );

        }


        renderCurrent();

        renderForecast();

        selectDay(
            Math.min(
                selectedDayIndex,
                14
            )
        );


    }

    catch (error) {

        console.error(error);


        document
            .getElementById(
                "currentWeather"
            )
            .innerHTML = `
                <div class="error">
                    Δεν ήταν δυνατή η φόρτωση
                    των δεδομένων καιρού.
                </div>
            `;

    }

}


/* =========================================================
   ΤΡΕΧΩΝ ΚΑΙΡΟΣ
========================================================= */

function renderCurrent() {


    const current =
        weatherData.current;


    /*
       Χρησιμοποιούμε το πραγματικό
       current block του API και όχι
       την πρώτη ώρα του forecast.
    */


    const temp =
        Math.round(
            current.temperature_2m
        );


    const feels =
        Math.round(
            current.apparent_temperature
        );


    const humidity =
        Math.round(
            current.relative_humidity_2m
        );


    const wind =
        Math.round(
            current.wind_speed_10m
        );


    const direction =
        windDirection(
            current.wind_direction_10m
        );


    /*
       Το current API δεν χρειάζεται να
       έχει πιθανότητα υετού.
       Χρησιμοποιούμε την τρέχουσα
       precipitation τιμή για να
       προστατεύουμε το εικονίδιο.
    */

    const currentPrecipitation =
        Number(
            current.precipitation || 0
        );


    const hourly =
        weatherData.hourly;


    const now =
        new Date();


    let nearestIndex = 0;

    let smallestDifference =
        Infinity;


    for (
        let i = 0;
        i < hourly.time.length;
        i++
    ) {

        const t =
            new Date(
                hourly.time[i]
            );


        const difference =
            Math.abs(
                t.getTime() -
                now.getTime()
            );


        if (
            difference <
            smallestDifference
        ) {

            smallestDifference =
                difference;

            nearestIndex =
                i;

        }

    }


    const probability =
        hourly
            .precipitation_probability[
                nearestIndex
            ] ?? 0;


    const code =
        current.weather_code;


    const isDay =
        current.is_day === 1;


    const info =
        weatherInfo(
            code,
            isDay,
            Math.max(
                Number(probability),
                currentPrecipitation > 0
                    ? 30
                    : 0
            )
        );


    document
        .getElementById(
            "currentWeather"
        )
        .innerHTML = `

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
                    <strong>
                        ${humidity}%
                    </strong>
                </div>

                <div class="info">
                    🌡️ Αίσθηση
                    <strong>
                        ${feels}°C
                    </strong>
                </div>

                <div class="info">
                    💨 Άνεμος
                    <strong>
                        ${wind} km/h
                        ${direction}
                    </strong>
                </div>

            </div>

        `;

}


/* =========================================================
   ΕΙΚΟΝΙΔΙΟ ΗΜΕΡΗΣΙΑΣ ΠΡΟΓΝΩΣΗΣ
========================================================= */

function dailyWeatherInfo(
    code,
    precipitationProbability
) {

    /*
       Τα daily cards αντιπροσωπεύουν
       κυρίως τη διάρκεια της ημέρας,
       οπότε χρησιμοποιούμε ημερήσια
       εικονίδια όταν δεν υπάρχει υετός.
    */

    return weatherInfo(
        code,
        true,
        precipitationProbability
    );

}


/* =========================================================
   15 ΗΜΕΡΕΣ
========================================================= */

function renderForecast() {


    const box =
        document.getElementById(
            "forecast"
        );


    box.innerHTML = "";


    const daily =
        weatherData.daily;


    for (
        let i = 0;
        i < 15;
        i++
    ) {


        const probability =
            daily
                .precipitation_probability_max[i]
                ?? 0;


        const info =
            dailyWeatherInfo(
                daily.weather_code[i],
                probability
            );


        const card =
            document.createElement(
                "div"
            );


        card.className =
            "day";


        if (
            i === selectedDayIndex
        ) {

            card.classList.add(
                "selected"
            );

        }


        card.innerHTML = `

            <div class="day-name">
                ${dayName(
                    daily.time[i]
                )}
            </div>

            <div class="date">
                ${formatDate(
                    daily.time[i]
                )}
            </div>

            <div class="day-icon">
                ${info[0]}
            </div>

            <div class="max">
                ${Math.round(
                    daily.temperature_2m_max[i]
                )}°
            </div>

            <div class="min">
                ${Math.round(
                    daily.temperature_2m_min[i]
                )}°
            </div>

            <div class="rain">
                💧 ${probability}%
            </div>

        `;


        card.onclick = () => {

            selectDay(i);

        };


        box.appendChild(
            card
        );

    }

}


/* =========================================================
   ΕΠΙΛΟΓΗ ΗΜΕΡΑΣ
========================================================= */

function selectDay(index) {


    if (
        !weatherData ||
        !weatherData.daily
    ) {

        return;

    }


    selectedDayIndex =
        index;


    renderForecast();

    renderHourlyDay(
        index
    );

}


/* =========================================================
   ΩΡΙΑΙΑ ΠΡΟΓΝΩΣΗ ΕΠΙΛΕΓΜΕΝΗΣ ΗΜΕΡΑΣ
========================================================= */

function renderHourlyDay(
    dayIndex
) {


    const hourly =
        weatherData.hourly;


    const daily =
        weatherData.daily;


    const selectedDate =
        daily.time[dayIndex];


    document
        .getElementById(
            "selectedDayTitle"
        )
        .textContent =

        "📅 " +

        dayName(
            selectedDate
        ) +

        " " +

        formatDate(
            selectedDate
        ) +

        " — Αναλυτική πρόγνωση";


    const box =
        document.getElementById(
            "hourly"
        );


    box.innerHTML = "";


    for (
        let i = 0;
        i < hourly.time.length;
        i++
    ) {


        const time =
            hourly.time[i];


        if (
            !time.startsWith(
                selectedDate
            )
        ) {

            continue;

        }


        const dateObject =
            new Date(time);


        const hour =
            dateObject
                .getHours()
                .toString()
                .padStart(
                    2,
                    "0"
                );


        const minute =
            dateObject
                .getMinutes()
                .toString()
                .padStart(
                    2,
                    "0"
                );


        const temperature =
            Math.round(
                hourly.temperature_2m[i]
            );


        const probability =
            hourly
                .precipitation_probability[i]
                ?? 0;


        const isDay =
            hourly.is_day[i] === 1;


        const info =
            weatherInfo(
                hourly.weather_code[i],
                isDay,
                probability
            );


        const wind =
            Math.round(
                hourly.wind_speed_10m[i]
            );


        const direction =
            windDirection(
                hourly.wind_direction_10m[i]
            );


        const row =
            document.createElement(
                "div"
            );


        row.className =
            "hour";


        row.innerHTML = `

            <div class="hour-time">
                ${hour}:${minute}
            </div>

            <div class="hour-icon">
                ${info[0]}
            </div>

            <div class="hour-condition">
                ${temperature}°C<br>
                ${info[1]}
            </div>

            <div class="hour-rain">
                💧 ${probability}%
            </div>

            <div class="wind">
                💨 ${wind} km/h<br>
                ${direction}
            </div>

        `;


        box.appendChild(
            row
        );

    }

}


/* =========================================================
   ΑΥΤΟΜΑΤΗ ΑΝΑΝΕΩΣΗ
========================================================= */

/*
   Κάθε 5 λεπτά ξαναζητάμε τα τελευταία
   διαθέσιμα δεδομένα.

   Δεν εμφανίζεται καμία σχετική ένδειξη
   στην ιστοσελίδα.
*/

setInterval(
    () => {

        loadWeather();

    },
    5 * 60 * 1000
);


/* =========================================================
   ΑΡΧΙΚΗ ΦΟΡΤΩΣΗ
========================================================= */

loadWeather();

</script>

</body>
</html>

Μία σημαντική διόρθωση που έκανα σε σχέση με τον προηγούμενο κώδικα: για την τρέχουσα θερμοκρασία χρησιμοποιείται πλέον το "current" του API και όχι αυθαίρετα η πρώτη ωριαία τιμή. Επίσης το "is_day" χρησιμοποιείται για να αποφασίζεται αν είναι ημέρα ή νύχτα, κάτι που το API παρέχει ως ξεχωριστό πεδίο.

Και το όριο των 30% εφαρμόζεται στην εμφάνιση των εικονιδίων υετού: η πιθανότητα υετού του Open-Meteo βασίζεται σε ensemble μοντέλα, με 30 διαφορετικές προσομοιώσεις.

Μικρή σημείωση: ο κώδικας χρησιμοποιεί "models=auto", όχι ένα αυθαίρετο μόνο μοντέλο. Αυτό είναι σκόπιμο, επειδή το ίδιο το API αναφέρει ότι το "Best Match" προσαρμόζει/συνδυάζει τα κατάλληλα διαθέσιμα μοντέλα για κάθε περιοχή παγκοσμίως.

Πες μου τώρα τις επόμενες αλλαγές που θέλεις και θα τις περάσουμε πάνω σε αυτόν τον πλήρη κώδικα.
