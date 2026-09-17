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
    color:white;
    min-height:100vh;
    background:linear-gradient(180deg,#022f58 0%,#012348 50%,#01172f 100%);
}

.container{
    width:94%;
    max-width:1200px;
    margin:auto;
    padding:25px 0 45px;
}

header{
    text-align:center;
    margin-bottom:22px;
}

.logo{
    font-size:32px;
    font-weight:800;
}

.subtitle{
    margin-top:5px;
    opacity:.8;
}

.search-area{
    max-width:700px;
    margin:22px auto;
}

.search-box{
    display:flex;
    background:white;
    border-radius:16px;
    overflow:hidden;
    box-shadow:0 8px 25px rgba(0,0,0,.35);
}

.search-box input{
    flex:1;
    min-width:0;
    border:0;
    outline:0;
    padding:16px;
    font-size:16px;
    color:#17324d;
}

.search-box button{
    border:0;
    background:#075db5;
    color:white;
    padding:0 22px;
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
}

.location{
    text-align:center;
    margin:15px 0 22px;
}

.location h1{
    font-size:30px;
}

.location p{
    margin-top:5px;
    opacity:.8;
}

.current{
    background:rgba(255,255,255,.10);
    border:1px solid rgba(255,255,255,.15);
    border-radius:24px;
    padding:25px;
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin-bottom:25px;
    box-shadow:0 10px 35px rgba(0,0,0,.30);
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
    margin:6px 0;
}

.section-title{
    font-size:23px;
    font-weight:700;
    margin:12px 0 14px;
}

/* ΑΚΡΙΒΩΣ 4 - 4 - 4 - 3 */
.forecast{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:12px;
}

.day{
    background:rgba(255,255,255,.10);
    border:1px solid rgba(255,255,255,.14);
    border-radius:20px;
    padding:17px 10px;
    text-align:center;
    cursor:pointer;
    transition:.2s;
}

.day:hover{
    transform:translateY(-3px);
    background:rgba(255,255,255,.17);
}

.day.active{
    background:white;
    color:#075db5;
}

.day-name{
    font-size:15px;
    font-weight:bold;
}

.day-date{
    font-size:13px;
    opacity:.7;
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
    font-size:14px;
    opacity:.65;
    margin-top:4px;
}

.rain{
    font-size:13px;
    margin-top:9px;
}

/* ΛΕΠΤΟΜΕΡΕΙΕΣ */
.details{
    margin-top:25px;
    background:rgba(255,255,255,.10);
    border:1px solid rgba(255,255,255,.15);
    border-radius:24px;
    padding:25px;
    box-shadow:0 10px 35px rgba(0,0,0,.30);
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
    background:rgba(0,0,0,.16);
    border-radius:15px;
    padding:15px;
}

.info-title{
    font-size:13px;
    opacity:.7;
    margin-bottom:6px;
}

.info-value{
    font-size:18px;
    font-weight:bold;
}

/* ΩΡΙΑΙΑ */
.hourly{
    display:flex;
    gap:10px;
    overflow-x:auto;
    padding-bottom:8px;
}

.hour{
    min-width:125px;
    background:rgba(0,0,0,.16);
    border-radius:16px;
    padding:14px 9px;
    text-align:center;
}

.hour-time{
    font-size:13px;
    opacity:.75;
}

.hour-icon{
    font-size:28px;
    margin:8px 0;
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

.hour-wind{
    font-size:13px;
    font-weight:bold;
    margin-top:8px;
}

.wind-direction{
    font-size:13px;
    margin-top:5px;
}

/* ΓΚΡΙ ΦΕΓΓΑΡΙ */
.moon{
    color:#b9bec5;
    filter:grayscale(1);
}

.loading{
    text-align:center;
    padding:40px;
    font-size:18px;
}

.error{
    background:rgba(180,0,0,.25);
    border:1px solid rgba(255,255,255,.25);
    padding:18px;
    border-radius:15px;
    text-align:center;
    margin:20px 0;
}

footer{
    text-align:center;
    margin-top:35px;
    opacity:.55;
    font-size:13px;
}


/* TABLET / PC */
@media (min-width:601px){
    .forecast{
        grid-template-columns:repeat(4,1fr);
    }

    /* Τα 3 τελευταία στην τελευταία σειρά */
    .day:nth-child(13){
        grid-column:1;
    }
}


/* ΚΙΝΗΤΟ */
@media (max-width:600px){

    .forecast{
        grid-template-columns:repeat(2,1fr);
    }

    .current{
        flex-direction:column;
        text-align:center;
        gap:20px;
    }

    .current-right{
        text-align:center;
    }

    .info-grid{
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
        <button id="searchButton">Αναζήτηση</button>
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


/* =========================
   ΚΑΙΡΙΚΑ ΕΙΚΟΝΙΔΙΑ
========================= */

function weatherInfo(code,isDay){

    if(!isDay){
        return ["🌙","Νύχτα",true];
    }

    switch(code){

        case 0:
            return ["☀️","Αίθριος",false];

        case 1:
            return ["🌤️","Κυρίως αίθριος",false];

        case 2:
            return ["⛅","Μερική συννεφιά",false];

        case 3:
            return ["☁️","Συννεφιά",false];

        case 45:
        case 48:
            return ["🌫️","Ομίχλη",false];

        case 51:
        case 53:
        case 55:
            return ["🌦️","Ψιλή βροχή",false];

        case 56:
        case 57:
        case 61:
        case 63:
        case 65:
            return ["🌧️","Βροχή",false];

        case 66:
        case 67:
            return ["🌧️","Παγωμένη βροχή",false];

        case 71:
        case 73:
        case 75:
        case 77:
            return ["🌨️","Χιόνι",false];

        case 80:
        case 81:
        case 82:
            return ["🌦️","Μπόρες",false];

        case 85:
        case 86:
            return ["🌨️","Χιονομπόρες",false];

        case 95:
            return ["⛈️","Καταιγίδα",false];

        case 96:
        case 99:
            return ["⛈️","Καταιγίδα με χαλάζι",false];

        default:
            return ["☁️","Μεταβλητός",false];
    }
}


/* =========================
   ΗΜΕΡΕΣ
========================= */

function getDayName(dateString){

    const names=[
        "Κυριακή",
        "Δευτέρα",
        "Τρίτη",
        "Τετάρτη",
        "Πέμπτη",
        "Παρασκευή",
        "Σάββατο"
    ];

    return names[
        new Date(dateString+"T12:00:00").getDay()
    ];
}


function getDate(dateString){

    return new Date(
        dateString+"T12:00:00"
    ).toLocaleDateString("el-GR",{
        day:"2-digit",
        month:"2-digit"
    });
}


/* =========================
   ΑΝΕΜΟΣ
========================= */

function getWindDirection(degrees){

    const directions=[
        "Β",
        "ΒΑ",
        "Α",
        "ΝΑ",
        "Ν",
        "ΝΔ",
        "Δ",
        "ΒΔ"
    ];

    const index=
        Math.round(degrees/45)%8;

    return directions[index];
}


function getWindArrow(degrees){

    /*
    Το βέλος περιστρέφεται ανάλογα
    με τη διεύθυνση του ανέμου.
    */

    return `
        <span style="
            display:inline-block;
            transform:rotate(${degrees}deg);
            font-size:21px;
        ">↑</span>
    `;
}


/* =========================
   ΑΝΑΖΗΤΗΣΗ ΠΕΡΙΟΧΗΣ
========================= */

async function searchLocation(){

    const input=
        document.getElementById("searchInput");

    const query=input.value.trim();

    if(!query){
        return;
    }

    document.getElementById("content").innerHTML=
        '<div class="loading">🔎 Αναζήτηση περιοχής...</div>';

    try{

        const url=
            "https://geocoding-api.open-meteo.com/v1/search"+
            "?name="+encodeURIComponent(query)+
            "&count=1"+
            "&language=el"+
            "&format=json";

        const response=await fetch(url);

        if(!response.ok){
            throw new Error("Geocoding failed");
        }

        const data=await response.json();

        if(!data.results || data.results.length===0){

            document.getElementById("content").innerHTML=
                '<div class="error">❌ Δεν βρέθηκε η περιοχή.</div>';

            return;
        }

        const place=data.results[0];

        await loadWeather(
            place.latitude,
            place.longitude,
            place.name,
            place.country || ""
        );

    }catch(error){

        console.error(error);

        document.getElementById("content").innerHTML=
            '<div class="error">❌ Δεν ήταν δυνατή η αναζήτηση. Δοκίμασε ξανά.</div>';
    }
}


/* =========================
   ΦΟΡΤΩΣΗ ΚΑΙΡΟΥ
========================= */

async function loadWeather(
    latitude,
    longitude,
    name,
    country
){

    document.getElementById("location").innerHTML=`
        <h1>📍 ${name}</h1>
        <p>${country}</p>
    `;

    document.getElementById("content").innerHTML=
        '<div class="loading">🌦️ Φόρτωση πρόγνωσης...</div>';

    try{

        /*
        Χρησιμοποιούμε το κανονικό Open-Meteo API.
        Δεν εξαρτάται από endpoint που μπορεί
        να μην είναι διαθέσιμο.
        */

        const url=
            "https://api.open-meteo.com/v1/forecast"+
            "?latitude="+latitude+
            "&longitude="+longitude+
            "&forecast_days=15"+
            "&timezone=auto"+
            "&temperature_unit=celsius"+
            "&wind_speed_unit=kmh"+
            "&precipitation_unit=mm"+

            "&daily="+
            "weather_code,"+
            "temperature_2m_max,"+
            "temperature_2m_min,"+
            "precipitation_sum,"+
            "precipitation_probability_max,"+
            "wind_speed_10m_max,"+
            "wind_gusts_10m_max,"+
            "wind_direction_10m_dominant,"+
            "sunrise,"+
            "sunset"+

            "&hourly="+
            "temperature_2m,"+
            "apparent_temperature,"+
            "precipitation_probability,"+
            "precipitation,"+
            "weather_code,"+
            "wind_speed_10m,"+
            "wind_direction_10m,"+
            "is_day";

        const response=await fetch(url);

        if(!response.ok){
            throw new Error("Weather request failed");
        }

        const data=await response.json();

        if(
            !data.daily ||
            !data.hourly ||
            !data.daily.time
        ){
            throw new Error("Incomplete weather data");
        }

        weatherData=data;
        selectedDay=0;

        renderWeather();

    }catch(error){

        console.error("WEATHER ERROR:",error);

        document.getElementById("content").innerHTML=
            '<div class="error">'+
            '❌ Δεν φορτώθηκαν τα δεδομένα καιρού.<br>'+
            '<small>Έλεγξε τη σύνδεση στο Internet και δοκίμασε ξανά.</small>'+
            '</div>';
    }
}


/* =========================
   ΚΥΡΙΑ ΠΡΟΒΟΛΗ
========================= */

function renderWeather(){

    const d=weatherData.daily;

    const todayInfo=
        weatherInfo(d.weather_code[0],true);

    document.getElementById("content").innerHTML=`

        <div class="current">

            <div class="current-left">

                <div class="current-icon">
                    ${todayInfo[0]}
                </div>

                <div>

                    <div class="current-temp">
                        ${Math.round(d.temperature_2m_max[0])}°
                    </div>

                    <div class="current-condition">
                        ${todayInfo[1]}
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

    renderDays();
    showDay(0);
}


/* =========================
   ΚΟΥΤΑΚΙΑ 15 ΗΜΕΡΩΝ
========================= */

function renderDays(){

    const d=weatherData.daily;

    const forecast=
        document.getElementById("forecast");

    forecast.innerHTML="";

    for(let i=0;i<15;i++){

        const info=
            weatherInfo(d.weather_code[i],true);

        const rain=
            d.precipitation_probability_max[i] ?? 0;

        const card=
            document.createElement("div");

        card.className="day";

        if(i===selectedDay){
            card.classList.add("active");
        }

        card.onclick=function(){
            showDay(i);
        };

        card.innerHTML=`

            <div class="day-name">
                ${i===0 ? "Σήμερα" : getDayName(d.time[i])}
            </div>

            <div class="day-date">
                ${getDate(d.time[i])}
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


/* =========================
   ΑΝΑΛΥΣΗ ΗΜΕΡΑΣ
========================= */

function showDay(index){

    selectedDay=index;

    renderDays();

    const d=weatherData.daily;
    const h=weatherData.hourly;

    const info=
        weatherInfo(d.weather_code[index],true);

    const rainProbability=
        d.precipitation_probability_max[index] ?? 0;

    const rainAmount=
        d.precipitation_sum[index] ?? 0;

    const sunrise=
        new Date(d.sunrise[index])
        .toLocaleTimeString("el-GR",{
            hour:"2-digit",
            minute:"2-digit"
        });

    const sunset=
        new Date(d.sunset[index])
        .toLocaleTimeString("el-GR",{
            hour:"2-digit",
            minute:"2-digit"
        });


    /* ΩΡΙΑΙΑ */
    let hourlyHTML="";

    for(let i=0;i<h.time.length;i++){

        if(h.time[i].startsWith(d.time[index])){

            const hour=
                new Date(h.time[i])
                .toLocaleTimeString("el-GR",{
                    hour:"2-digit",
                    minute:"2-digit"
                });

            const isDay=
                h.is_day[i]===1;

            const hourInfo=
                weatherInfo(
                    h.weather_code[i],
                    isDay
                );

            const windSpeed=
                Math.round(h.wind_speed_10m[i] ?? 0);

            const degrees=
                h.wind_direction_10m[i] ?? 0;

            const direction=
                getWindDirection(degrees);

            const arrow=
                getWindArrow(degrees);


            hourlyHTML+=`

                <div class="hour">

                    <div class="hour-time">
                        ${hour}
                    </div>

                    <div class="hour-icon ${
                        !isDay ? "moon" : ""
                    }">
                        ${hourInfo[0]}
                    </div>

                    <div class="hour-temp">
                        ${Math.round(h.temperature_2m[i])}°
                    </div>

                    <div class="hour-rain">
                        💧 ${h.precipitation_probability[i] ?? 0}%
                    </div>

                    <div class="hour-wind">
                        💨 ${windSpeed} km/h
                    </div>

                    <div class="wind-direction">
                        ${arrow} ${direction}
                    </div>

                </div>
            `;
        }
    }


    document.getElementById("details").innerHTML=`

        <div class="details">

            <div class="details-title">
                ${index===0 ? "Σήμερα" : getDayName(d.time[index])}
                · ${getDate(d.time[index])}
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
                        ${Math.round(d.wind_speed_10m_max[index])} km/h
                    </div>
                </div>

                <div class="info">
                    <div class="info-title">
                        💨 Ριπές
                    </div>
                    <div class="info-value">
                        ${Math.round(d.wind_gusts_10m_max[index])} km/h
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


            <div class="section-title" style="margin-top:28px">
                Ωριαία πρόγνωση · άνεμος
            </div>

            <div class="hourly">
                ${hourlyHTML}
            </div>

        </div>
    `;
}


/* =========================
   ΚΟΥΜΠΙ ΑΝΑΖΗΤΗΣΗΣ
========================= */

document
.getElementById("searchButton")
.addEventListener("click",searchLocation);


/* ENTER ΣΤΗΝ ΑΝΑΖΗΤΗΣΗ */

document
.getElementById("searchInput")
.addEventListener("keydown",function(event){

    if(event.key==="Enter"){
        searchLocation();
    }

});


/* =========================
   ΑΡΧΙΚΗ ΠΕΡΙΟΧΗ
========================= */

loadWeather(
    40.6401,
    22.9444,
    "Θεσσαλονίκη",
    "Ελλάδα"
);

</script>

</body>
</html>
