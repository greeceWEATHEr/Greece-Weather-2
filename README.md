<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<style>
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
}

body{
    font-family:Arial,Helvetica,sans-serif;
    background:linear-gradient(180deg,#0477d9 0%,#075db5 45%,#063f83 100%);
    color:white;
    min-height:100vh;
}

.container{
    width:94%;
    max-width:1200px;
    margin:auto;
    padding:25px 0 45px;
}

/* HEADER */

header{
    text-align:center;
    margin-bottom:22px;
}

.logo{
    font-size:32px;
    font-weight:800;
    letter-spacing:.5px;
}

.subtitle{
    opacity:.85;
    margin-top:5px;
}

/* SEARCH */

.search-area{
    display:flex;
    justify-content:center;
    margin:22px auto;
    max-width:700px;
    gap:8px;
}

.search-box{
    flex:1;
    display:flex;
    background:white;
    border-radius:16px;
    overflow:hidden;
    box-shadow:0 8px 25px rgba(0,0,0,.2);
}

.search-box input{
    flex:1;
    border:none;
    outline:none;
    padding:16px;
    font-size:16px;
    color:#17324d;
}

.search-box button{
    border:none;
    background:#075db5;
    color:white;
    padding:0 22px;
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
}

.search-box button:hover{
    background:#064a91;
}

/* LOCATION */

.location{
    text-align:center;
    margin:15px 0 22px;
}

.location h1{
    font-size:30px;
}

.location p{
    opacity:.85;
    margin-top:5px;
}

/* CURRENT WEATHER */

.current{
    background:rgba(255,255,255,.14);
    backdrop-filter:blur(12px);
    border:1px solid rgba(255,255,255,.2);
    border-radius:24px;
    padding:25px;
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin-bottom:25px;
    box-shadow:0 10px 35px rgba(0,0,0,.15);
}

.current-left{
    display:flex;
    align-items:center;
    gap:18px;
}

.current-icon{
    font-size:65px;
}

.current-temp{
    font-size:58px;
    font-weight:800;
}

.current-condition{
    font-size:18px;
    opacity:.9;
}

.current-right{
    text-align:right;
}

.current-right div{
    margin:5px 0;
    opacity:.9;
}

/* FORECAST */

.section-title{
    font-size:23px;
    font-weight:700;
    margin:10px 0 14px;
}

.forecast{
    display:grid;
    grid-template-columns:repeat(5,1fr);
    gap:12px;
}

.day{
    background:rgba(255,255,255,.13);
    border:1px solid rgba(255,255,255,.18);
    border-radius:20px;
    padding:17px 10px;
    text-align:center;
    cursor:pointer;
    transition:.2s;
}

.day:hover{
    transform:translateY(-4px);
    background:rgba(255,255,255,.22);
}

.day.active{
    background:white;
    color:#075db5;
    box-shadow:0 8px 25px rgba(0,0,0,.22);
}

.day-name{
    font-size:15px;
    font-weight:bold;
}

.day-date{
    font-size:13px;
    opacity:.75;
    margin-top:4px;
}

.day-icon{
    font-size:40px;
    margin:12px 0;
}

.day-temp{
    font-size:21px;
    font-weight:bold;
}

.day-min{
    opacity:.65;
    font-size:14px;
    margin-top:4px;
}

.rain{
    margin-top:9px;
    font-size:13px;
    opacity:.85;
}

/* DETAILS */

.details{
    margin-top:25px;
    background:rgba(255,255,255,.14);
    backdrop-filter:blur(12px);
    border:1px solid rgba(255,255,255,.2);
    border-radius:24px;
    padding:25px;
    box-shadow:0 10px 35px rgba(0,0,0,.15);
}

.details-title{
    font-size:25px;
    font-weight:bold;
    margin-bottom:18px;
}

.details-main{
    display:flex;
    align-items:center;
    gap:20px;
    margin-bottom:22px;
}

.details-icon{
    font-size:65px;
}

.details-temperature{
    font-size:45px;
    font-weight:800;
}

.details-condition{
    font-size:17px;
    opacity:.9;
}

.info-grid{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:12px;
}

.info{
    background:rgba(0,0,0,.12);
    border-radius:15px;
    padding:15px;
}

.info-title{
    opacity:.7;
    font-size:13px;
    margin-bottom:6px;
}

.info-value{
    font-size:18px;
    font-weight:bold;
}

/* HOURLY */

.hourly{
    display:flex;
    gap:10px;
    overflow-x:auto;
    padding-bottom:5px;
}

.hour{
    min-width:105px;
    background:rgba(0,0,0,.12);
    border-radius:16px;
    padding:14px 9px;
    text-align:center;
}

.hour-time{
    font-size:13px;
    opacity:.75;
}

.hour-icon{
    font-size:27px;
    margin:9px 0;
}

.hour-temp{
    font-size:18px;
    font-weight:bold;
}

.hour-rain{
    font-size:12px;
    opacity:.75;
    margin-top:5px;
}

/* LOADING */

.loading{
    text-align:center;
    padding:40px;
    font-size:18px;
}

.error{
    background:rgba(220,0,0,.25);
    border:1px solid rgba(255,255,255,.25);
    padding:18px;
    border-radius:15px;
    text-align:center;
    margin:20px 0;
}

/* FOOTER */

footer{
    text-align:center;
    margin-top:35px;
    opacity:.65;
    font-size:13px;
}

/* MOBILE */

@media(max-width:850px){
    .forecast{
        grid-template-columns:repeat(3,1fr);
    }

    .info-grid{
        grid-template-columns:repeat(2,1fr);
    }

    .current{
        flex-direction:column;
        gap:20px;
        text-align:center;
    }

    .current-right{
        text-align:center;
    }
}

@media(max-width:520px){
    .container{
        width:96%;
        padding-top:18px;
    }

    .logo{
        font-size:26px;
    }

    .forecast{
        grid-template-columns:repeat(2,1fr);
    }

    .current-temp{
        font-size:48px;
    }

    .current-icon{
        font-size:55px;
    }

    .details{
        padding:18px;
    }

    .details-temperature{
        font-size:37px;
    }
}
</style>
</head>

<body>

<div class="container">

<header>
    <div class="logo">🌤️ Greece Weather</div>
    <div class="subtitle">15ήμερη πρόγνωση καιρού</div>
</header>

<div class="search-area">
    <div class="search-box">
        <input
            id="searchInput"
            type="text"
            placeholder="Αναζήτησε πόλη ή περιοχή..."
            autocomplete="off"
        >
        <button onclick="searchLocation()">Αναζήτηση</button>
    </div>
</div>

<div id="location" class="location"></div>

<div id="content">
    <div class="loading">⏳ Φόρτωση καιρού...</div>
</div>

<footer>
    Weather data powered by Open-Meteo
</footer>

</div>


<script>

let weatherData = null;
let selectedDay = 0;


/* -----------------------------
   WEATHER ICONS
----------------------------- */

function weatherInfo(code){

    if(code === 0)
        return ["☀️","Αίθριος"];

    if(code === 1)
        return ["🌤️","Κυρίως αίθριος"];

    if(code === 2)
        return ["⛅","Μερική συννεφιά"];

    if(code === 3)
        return ["☁️","Συννεφιά"];

    if([45,48].includes(code))
        return ["🌫️","Ομίχλη"];

    if([51,53,55].includes(code))
        return ["🌦️","Ψιλή βροχή"];

    if([56,57].includes(code))
        return ["🌧️","Παγωμένη βροχή"];

    if([61,63,65].includes(code))
        return ["🌧️","Βροχή"];

    if([66,67].includes(code))
        return ["🌧️","Παγωμένη βροχή"];

    if([71,73,75,77].includes(code))
        return ["🌨️","Χιονόπτωση"];

    if([80,81,82].includes(code))
        return ["🌦️","Μπόρες"];

    if([85,86].includes(code))
        return ["🌨️","Χιονομπόρες"];

    if([95].includes(code))
        return ["⛈️","Καταιγίδα"];

    if([96,99].includes(code))
        return ["⛈️","Καταιγίδα με χαλάζι"];

    return ["🌤️","Μεταβλητός"];
}


/* -----------------------------
   DATE
----------------------------- */

function dayName(dateString){

    const days = [
        "Κυριακή",
        "Δευτέρα",
        "Τρίτη",
        "Τετάρτη",
        "Πέμπτη",
        "Παρασκευή",
        "Σάββατο"
    ];

    const date = new Date(dateString + "T12:00:00");

    return days[date.getDay()];
}


function formatDate(dateString){

    const date = new Date(dateString + "T12:00:00");

    return date.toLocaleDateString("el-GR",{
        day:"2-digit",
        month:"2-digit"
    });
}


/* -----------------------------
   SEARCH LOCATION
----------------------------- */

async function searchLocation(){

    const input = document.getElementById("searchInput");

    const query = input.value.trim();

    if(!query){
        return;
    }

    document.getElementById("content").innerHTML =
        '<div class="loading">🔎 Αναζήτηση περιοχής...</div>';

    try{

        const geoURL =
            "https://geocoding-api.open-meteo.com/v1/search" +
            "?name=" + encodeURIComponent(query) +
            "&count=1" +
            "&language=el" +
            "&format=json";

        const geoResponse = await fetch(geoURL);

        if(!geoResponse.ok){
            throw new Error("Geocoding error");
        }

        const geoData = await geoResponse.json();

        if(!geoData.results || geoData.results.length === 0){

            document.getElementById("content").innerHTML =
                '<div class="error">❌ Δεν βρέθηκε η περιοχή.</div>';

            return;
        }

        const place = geoData.results[0];

        await loadWeather(
            place.latitude,
            place.longitude,
            place.name,
            place.country
        );

    }catch(error){

        console.error(error);

        document.getElementById("content").innerHTML =
            '<div class="error">❌ Δεν ήταν δυνατή η φόρτωση των δεδομένων. Δοκίμασε ξανά.</div>';
    }
}


/* -----------------------------
   LOAD WEATHER
----------------------------- */

async function loadWeather(lat,lon,name,country){

    document.getElementById("location").innerHTML =
        "<h1>📍 " + name + "</h1>" +
        "<p>" + (country || "") + "</p>";

    document.getElementById("content").innerHTML =
        '<div class="loading">🌦️ Φόρτωση πρόγνωσης...</div>';

    try{

        /*
        ECMWF IFS:
        πραγματική παγκόσμια πρόγνωση έως 15 ημέρες.
        */

        const url =
            "https://api.open-meteo.com/v1/ecmwf" +
            "?latitude=" + lat +
            "&longitude=" + lon +
            "&forecast_days=15" +
            "&timezone=auto" +
            "&temperature_unit=celsius" +
            "&wind_speed_unit=kmh" +
            "&precipitation_unit=mm" +

            "&daily=" +
            "weather_code," +
            "temperature_2m_max," +
            "temperature_2m_min," +
            "precipitation_sum," +
            "precipitation_probability_max," +
            "wind_speed_10m_max," +
            "wind_gusts_10m_max," +
            "wind_direction_10m_dominant," +
            "sunrise," +
            "sunset" +

            "&hourly=" +
            "temperature_2m," +
            "apparent_temperature," +
            "precipitation_probability," +
            "precipitation," +
            "weather_code," +
            "wind_speed_10m";

        const response = await fetch(url);

        if(!response.ok){
            throw new Error("Weather API error");
        }

        weatherData = await response.json();

        selectedDay = 0;

        renderWeather();

    }catch(error){

        console.error(error);

        document.getElementById("content").innerHTML =
            '<div class="error">❌ Δεν φορτώθηκαν τα δεδομένα καιρού.</div>';
    }
}


/* -----------------------------
   RENDER WEATHER
----------------------------- */

function renderWeather(){

    const d = weatherData.daily;

    const firstCode = d.weather_code[0];

    const info = weatherInfo(firstCode);

    const html = `

    <div class="current">

        <div class="current-left">

            <div class="current-icon">
                ${info[0]}
            </div>

            <div>

                <div class="current-temp">
                    ${Math.round(d.temperature_2m_max[0])}°
                </div>

                <div class="current-condition">
                    ${info[1]}
                </div>

            </div>

        </div>

        <div class="current-right">

            <div>
                🌡️ Ελάχιστη:
                <b>${Math.round(d.temperature_2m_min[0])}°C</b>
            </div>

            <div>
                💧 Βροχή:
                <b>${d.precipitation_probability_max[0] ?? 0}%</b>
            </div>

            <div>
                💨 Άνεμος:
                <b>${Math.round(d.wind_speed_10m_max[0])} km/h</b>
            </div>

        </div>

    </div>


    <div class="section-title">
        15ήμερη πρόγνωση
    </div>

    <div id="forecast" class="forecast"></div>

    <div id="details"></div>

    `;

    document.getElementById("content").innerHTML = html;

    renderDays();

    showDay(0);
}


/* -----------------------------
   15 DAYS
----------------------------- */

function renderDays(){

    const d = weatherData.daily;

    const forecast = document.getElementById("forecast");

    forecast.innerHTML = "";

    for(let i=0;i<15;i++){

        const info = weatherInfo(d.weather_code[i]);

        const rain = d.precipitation_probability_max[i] ?? 0;

        const card = document.createElement("div");

        card.className = "day";

        if(i === selectedDay){
            card.classList.add("active");
        }

        card.onclick = function(){
            showDay(i);
        };

        card.innerHTML = `

            <div class="day-name">
                ${i === 0 ? "Σήμερα" : dayName(d.time[i])}
            </div>

            <div class="day-date">
                ${formatDate(d.time[i])}
            </div>

            <div class="day-icon">
                ${info[0]}
            </div>

            <div class="day-temp">
                ${Math.round(d.temperature_2m_max[i])}°
            </div>

            <div class="day-min">
                ${Math.round(d.temperature_2m_min[i])}°
            </div>

            <div class="rain">
                💧 ${rain}%
            </div>

        `;

        forecast.appendChild(card);
    }
}


/* -----------------------------
   SELECT DAY
----------------------------- */

function showDay(index){

    selectedDay = index;

    renderDays();

    const d = weatherData.daily;

    const info = weatherInfo(d.weather_code[index]);

    const rainProbability =
        d.precipitation_probability_max[index] ?? 0;

    const rainAmount =
        d.precipitation_sum[index] ?? 0;

    const sunrise =
        new Date(d.sunrise[index]).toLocaleTimeString("el-GR",{
            hour:"2-digit",
            minute:"2-digit"
        });

    const sunset =
        new Date(d.sunset[index]).toLocaleTimeString("el-GR",{
            hour:"2-digit",
            minute:"2-digit"
        });


    let hourlyHTML = "";

    /*
    Find the hourly entries belonging to this date.
    */

    for(let h=0; h<weatherData.hourly.time.length; h++){

        const time = weatherData.hourly.time[h];

        if(time.startsWith(d.time[index])){

            const hour =
                new Date(time).toLocaleTimeString("el-GR",{
                    hour:"2-digit"
                });

            const hourInfo =
                weatherInfo(weatherData.hourly.weather_code[h]);

            hourlyHTML += `

                <div class="hour">

                    <div class="hour-time">
                        ${hour}
                    </div>

                    <div class="hour-icon">
                        ${hourInfo[0]}
                    </div>

                    <div class="hour-temp">
                        ${Math.round(
                            weatherData.hourly.temperature_2m[h]
                        )}°
                    </div>

                    <div class="hour-rain">
                        💧 ${
                            weatherData.hourly.precipitation_probability[h] ?? 0
                        }%
                    </div>

                </div>

            `;
        }
    }


    const detailsHTML = `

        <div class="details">

            <div class="details-title">
                ${index === 0 ? "Σήμερα" : dayName(d.time[index])}
                · ${formatDate(d.time[index])}
            </div>

            <div class="details-main">

                <div class="details-icon">
                    ${info[0]}
                </div>

                <div>

                    <div class="details-temperature">
                        ${Math.round(d.temperature_2m_max[index])}°
                    </div>

                    <div class="details-condition">
                        ${info[1]}
                    </div>

                </div>

            </div>


            <div class="info-grid">

                <div class="info">
                    <div class="info-title">
                        🌡️ Θερμοκρασία
                    </div>

                    <div class="info-value">
                        ${Math.round(d.temperature_2m_min[index])}°
                        —
                        ${Math.round(d.temperature_2m_max[index])}°C
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        🌧️ Πιθανότητα βροχής
                    </div>

                    <div class="info-value">
                        ${rainProbability}%
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        💧 Υετός
                    </div>

                    <div class="info-value">
                        ${rainAmount.toFixed(1)} mm
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        💨 Μέγιστος άνεμος
                    </div>

                    <div class="info-value">
                        ${Math.round(d.wind_speed_10m_max[index])}
                        km/h
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        💨 Ριπές
                    </div>

                    <div class="info-value">
                        ${Math.round(d.wind_gusts_10m_max[index])}
                        km/h
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        🌅 Ανατολή
                    </div>

                    <div class="info-value">
                        ${sunrise}
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        🌇 Δύση
                    </div>

                    <div class="info-value">
                        ${sunset}
                    </div>
                </div>

            </div>


            <div class="section-title" style="margin-top:28px;">
                Ωριαία πρόγνωση
            </div>

            <div class="hourly">
                ${hourlyHTML}
            </div>

        </div>

    `;

    document.getElementById("details").innerHTML = detailsHTML;
}


/* -----------------------------
   ENTER KEY
----------------------------- */

document
.getElementById("searchInput")
.addEventListener("keydown",function(event){

    if(event.key === "Enter"){
        searchLocation();
    }

});


/* -----------------------------
   START
   Thessaloniki
----------------------------- */

loadWeather(
    40.6401,
    22.9444,
    "Θεσσαλονίκη",
    "Ελλάδα"
);

</script>

</body>
</html>
