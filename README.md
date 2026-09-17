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
    background:#06284a;
    color:white;
    min-height:100vh;
}

.container{
    width:94%;
    max-width:1100px;
    margin:auto;
    padding:25px 0 40px;
}

/* HEADER */

header{
    background:#031d38;
    padding:28px 20px;
    text-align:center;
    border-bottom:1px solid #a9b8c8;
    margin-bottom:22px;
}

.logo{
    font-size:31px;
    font-weight:bold;
}

.subtitle{
    margin-top:12px;
    color:#cbd6e2;
    font-size:18px;
}

/* SEARCH */

.search{
    display:flex;
    gap:12px;
    margin-bottom:25px;
}

.search input{
    flex:1;
    min-width:0;
    border:none;
    border-radius:17px;
    padding:18px;
    font-size:17px;
    outline:none;
}

.search button{
    border:none;
    border-radius:17px;
    padding:0 24px;
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
}

/* LOCATION */

.location{
    text-align:center;
    margin-bottom:20px;
}

.location h1{
    font-size:30px;
    margin-bottom:5px;
}

.location .country{
    color:#c7d3df;
    font-size:18px;
}

/* CURRENT */

.current{
    background:#345577;
    border-radius:24px;
    padding:25px 28px;
    text-align:center;
    margin-bottom:30px;
}

.current-title{
    font-size:30px;
    font-weight:bold;
    padding-bottom:15px;
    border-bottom:1px solid #b9c7d5;
}

.current-temp{
    font-size:62px;
    font-weight:300;
    margin-top:20px;
}

.current-condition{
    font-size:20px;
    margin:8px 0 24px;
}

.current-info{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:14px;
}

.current-box{
    background:#527293;
    border-radius:16px;
    padding:15px;
    color:#e5edf5;
}

.current-box .label{
    font-size:17px;
    margin-bottom:9px;
}

.current-box .value{
    font-size:17px;
    font-weight:bold;
}

/* SECTION TITLE */

.section-title{
    font-size:26px;
    font-weight:bold;
    padding-bottom:15px;
    border-bottom:1px solid #aebdca;
    margin-bottom:18px;
}

/* 15 DAY */

.forecast{
    display:grid;
    grid-template-columns:repeat(6,1fr);
    gap:14px;
    margin-bottom:30px;
}

.day{
    background:#345577;
    border-radius:18px;
    padding:17px 8px;
    text-align:center;
    cursor:pointer;
    transition:.2s;
}

.day:hover{
    transform:translateY(-2px);
    background:#3c6286;
}

.day.active{
    background:#416587;
    outline:2px solid #9bb2c8;
}

.day-name{
    font-size:16px;
    font-weight:bold;
}

.day-date{
    margin-top:9px;
    font-size:14px;
    color:#d1dce7;
}

.day-icon{
    font-size:45px;
    margin:16px 0;
}

.day-max{
    font-size:21px;
    font-weight:bold;
}

.day-min{
    margin-top:7px;
    font-size:16px;
    color:#d0dbe6;
}

.day-rain{
    margin-top:14px;
    font-size:14px;
    color:#e3edf6;
}

/* DETAILS */

.details{
    background:#031d38;
    border-radius:24px;
    padding:25px;
    margin-top:20px;
}

.details-header{
    display:flex;
    justify-content:space-between;
    align-items:center;
    border-bottom:1px solid #aab9c8;
    padding-bottom:16px;
    margin-bottom:18px;
}

.details-title{
    font-size:23px;
    font-weight:bold;
}

.close-btn{
    background:#345577;
    color:white;
    border:0;
    border-radius:12px;
    padding:12px 18px;
    font-size:15px;
    cursor:pointer;
}

/* HOURLY */

.hourly{
    display:flex;
    flex-direction:column;
    gap:10px;
}

.hour{
    background:#345577;
    border-radius:15px;
    min-height:74px;
    padding:12px;

    display:grid;
    grid-template-columns:
        90px
        80px
        1fr
        1fr;

    align-items:center;
}

.hour-time{
    font-size:18px;
    font-weight:bold;
}

.hour-icon{
    font-size:34px;
    text-align:center;
}

.hour-temp{
    font-size:15px;
    line-height:1.6;
}

.hour-rain{
    font-size:15px;
    line-height:1.6;
}

.hour-wind{
    font-size:15px;
    line-height:1.6;
}

/* LOADING */

.loading{
    text-align:center;
    padding:40px;
    font-size:19px;
}

/* ERROR */

.error{
    background:#4b2630;
    border-radius:18px;
    padding:22px;
    text-align:center;
}

/* RESPONSIVE */

@media(max-width:850px){

    .forecast{
        grid-template-columns:repeat(4,1fr);
    }

}

@media(max-width:600px){

    .container{
        width:94%;
    }

    .logo{
        font-size:27px;
    }

    .search{
        gap:8px;
    }

    .search button{
        padding:0 15px;
    }

    .current-info{
        grid-template-columns:1fr;
    }

    .forecast{
        grid-template-columns:repeat(3,1fr);
    }

    .current-temp{
        font-size:52px;
    }

    .hour{
        grid-template-columns:
            65px
            55px
            1fr
            1fr;
    }

    .hour-time{
        font-size:15px;
    }

    .hour-icon{
        font-size:27px;
    }

    .hour-temp,
    .hour-rain,
    .hour-wind{
        font-size:13px;
    }

}

</style>
</head>

<body>

<div class="container">

<header>

    <div class="logo">
        🇬🇷 Greece Weather
    </div>

    <div class="subtitle">
        Πρόγνωση καιρού για όλη την Ελλάδα
    </div>

</header>


<div class="search">

    <input
        id="searchInput"
        type="text"
        placeholder="Αναζήτησε πόλη ή περιοχή..."
    >

    <button id="searchButton">
        Αναζήτηση
    </button>

</div>


<div id="location" class="location"></div>


<div id="content">

    <div class="loading">
        ⏳ Φόρτωση δεδομένων...
    </div>

</div>


</div>


<script>

/* ============================
   ΜΕΤΑΒΛΗΤΕΣ
============================ */

let weatherData = null;
let selectedDay = 0;


/* ============================
   ΚΑΙΡΙΚΑ ΕΙΚΟΝΙΔΙΑ
============================ */

function weatherInfo(code,isDay){

    /* ΝΥΧΤΑ */

    if(!isDay){

        if(code === 0)
            return ["🌙","Ξαστεριά"];

        if(code === 1)
            return ["🌙","Κυρίως αίθριος"];

        if(code === 2)
            return ["☁️","Μερική συννεφιά"];

        if(code === 3)
            return ["☁️","Συννεφιά"];

        if(code === 45 || code === 48)
            return ["🌫️","Ομίχλη"];

        if(code >= 51 && code <= 55)
            return ["🌧️","Ψιλή βροχή"];

        if(code >= 61 && code <= 67)
            return ["🌧️","Βροχή"];

        if(code >= 71 && code <= 77)
            return ["🌨️","Χιόνι"];

        if(code >= 80 && code <= 82)
            return ["🌧️","Μπόρες"];

        if(code === 85 || code === 86)
            return ["🌨️","Χιονομπόρες"];

        if(code >= 95)
            return ["⛈️","Καταιγίδα"];

        return ["☁️","Συννεφιά"];
    }


    /* ΗΜΕΡΑ */

    if(code === 0)
        return ["☀️","Αίθριος"];

    if(code === 1)
        return ["🌤️","Κυρίως αίθριος"];

    if(code === 2)
        return ["⛅","Μερική συννεφιά"];

    if(code === 3)
        return ["☁️","Συννεφιά"];

    if(code === 45 || code === 48)
        return ["🌫️","Ομίχλη"];

    if(code >= 51 && code <= 55)
        return ["🌦️","Ψιλή βροχή"];

    if(code >= 61 && code <= 67)
        return ["🌧️","Βροχή"];

    if(code >= 71 && code <= 77)
        return ["🌨️","Χιόνι"];

    if(code >= 80 && code <= 82)
        return ["🌦️","Μπόρες"];

    if(code === 85 || code === 86)
        return ["🌨️","Χιονομπόρες"];

    if(code >= 95)
        return ["⛈️","Καταιγίδα"];

    return ["☁️","Μεταβλητός"];
}


/* ============================
   ΗΜΕΡΑ
============================ */

function getDayName(date){

    const names = [
        "Κυρ",
        "Δευ",
        "Τρί",
        "Τετ",
        "Πέμ",
        "Παρ",
        "Σάβ"
    ];

    return names[
        new Date(date+"T12:00:00").getDay()
    ];
}


/* ============================
   ΗΜΕΡΟΜΗΝΙΑ
============================ */

function getDate(date){

    return new Date(
        date+"T12:00:00"
    ).toLocaleDateString(
        "el-GR",
        {
            day:"2-digit",
            month:"2-digit"
        }
    );
}


/* ============================
   ΑΝΕΜΟΣ
============================ */

function getWindDirection(degrees){

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

    return directions[
        Math.round(degrees/45)%8
    ];
}


/* ============================
   ΥΕΤΟΣ
============================ */

function rainIcon(probability){

    if(probability >= 30){
        return " 🌧️";
    }

    return "";
}


/* ============================
   ΑΝΑΖΗΤΗΣΗ
============================ */

async function searchLocation(){

    const input =
        document.getElementById("searchInput");

    const query =
        input.value.trim();

    if(!query){
        return;
    }

    document.getElementById("content").innerHTML =
        '<div class="loading">🔎 Αναζήτηση...</div>';

    try{

        const url =
            "https://geocoding-api.open-meteo.com/v1/search" +
            "?name="+encodeURIComponent(query) +
            "&count=1" +
            "&language=el" +
            "&format=json";

        const response =
            await fetch(url);

        if(!response.ok){
            throw new Error();
        }

        const data =
            await response.json();

        if(!data.results ||
           data.results.length === 0){

            document.getElementById("content").innerHTML =
                '<div class="error">❌ Η περιοχή δεν βρέθηκε.</div>';

            return;
        }

        const place =
            data.results[0];

        await loadWeather(
            place.latitude,
            place.longitude,
            place.name,
            place.country || ""
        );

    }catch(error){

        console.error(error);

        document.getElementById("content").innerHTML =
            '<div class="error">❌ Δεν ήταν δυνατή η αναζήτηση.</div>';
    }
}


/* ============================
   ΦΟΡΤΩΣΗ ΚΑΙΡΟΥ
============================ */

async function loadWeather(
    latitude,
    longitude,
    name,
    country
){

    document.getElementById("location").innerHTML =

        "<h1>"+name+"</h1>" +

        '<div class="country">'+
        country+
        "</div>";


    document.getElementById("content").innerHTML =
        '<div class="loading">🌦️ Φόρτωση πρόγνωσης...</div>';


    try{

        const url =

            "https://api.open-meteo.com/v1/forecast" +

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


        const response =
            await fetch(url);


        if(!response.ok){
            throw new Error();
        }


        const data =
            await response.json();


        weatherData = data;

        selectedDay = 0;

        renderWeather();


    }catch(error){

        console.error(error);

        document.getElementById("content").innerHTML =
            '<div class="error">'+
            '❌ Δεν φορτώθηκαν τα δεδομένα καιρού.'+
            '<br><br>'+
            'Δοκίμασε ξανά.'+
            '</div>';
    }
}


/* ============================
   ΚΥΡΙΑ ΠΡΟΒΟΛΗ
============================ */

function renderWeather(){

    const d =
        weatherData.daily;

    const h =
        weatherData.hourly;


    /*
       Τρέχουσα ώρα:
       χρησιμοποιούμε τον πρώτο
       διαθέσιμο ωριαίο κωδικό.
    */

    const currentCode =
        h.weather_code[0];

    const currentIsDay =
        h.is_day[0] === 1;

    const info =
        weatherInfo(
            currentCode,
            currentIsDay
        );


    const currentTemp =
        Math.round(
            h.temperature_2m[0]
        );


    const currentFeels =
        Math.round(
            h.apparent_temperature[0]
        );


    const currentWind =
        Math.round(
            h.wind_speed_10m[0]
        );


    const currentDirection =
        getWindDirection(
            h.wind_direction_10m[0]
        );


    const currentHumidity =
        h.relative_humidity_2m
        ? h.relative_humidity_2m[0]
        : null;


    document.getElementById("content").innerHTML = `

        <div class="current">

            <div class="current-title">
                ${document.querySelector(".location h1").textContent}
            </div>

            <div class="current-temp">
                ${currentTemp}°C
            </div>

            <div class="current-condition">
                ${info[0]} ${info[1]}
            </div>


            <div class="current-info">

                <div class="current-box">

                    <div class="label">
                        💧 Υγρασία
                    </div>

                    <div class="value">
                        ${
                            currentHumidity !== null
                            ? currentHumidity+"%"
                            : "—"
                        }
                    </div>

                </div>


                <div class="current-box">

                    <div class="label">
                        💨 Άνεμος
                    </div>

                    <div class="value">
                        ${currentWind} km/h — ${currentDirection}
                    </div>

                </div>


                <div class="current-box">

                    <div class="label">
                        🌡️ Αίσθηση
                    </div>

                    <div class="value">
                        ${currentFeels}°C
                    </div>

                </div>

            </div>

        </div>


        <div class="section-title">
            📅 Πρόγνωση 15 ημερών
        </div>


        <div id="forecast" class="forecast"></div>


        <div id="details"></div>

    `;


    renderDays();

    showDay(0);
}


/* ============================
   15 ΗΜΕΡΕΣ
============================ */

function renderDays(){

    const d =
        weatherData.daily;

    const forecast =
        document.getElementById("forecast");


    forecast.innerHTML = "";


    for(let i=0;i<15;i++){

        const info =
            weatherInfo(
                d.weather_code[i],
                true
            );


        const rain =
            d.precipitation_probability_max[i] ?? 0;


        const card =
            document.createElement("div");


        card.className = "day";


        if(i === selectedDay){
            card.classList.add("active");
        }


        card.onclick = function(){

            showDay(i);

        };


        card.innerHTML = `

            <div class="day-name">

                ${
                    i === 0
                    ? "Σήμερα"
                    : getDayName(d.time[i])
                }

            </div>


            <div class="day-date">
                ${getDate(d.time[i])}
            </div>


            <div class="day-icon">
                ${info[0]}
            </div>


            <div class="day-max">
                ${Math.round(
                    d.temperature_2m_max[i]
                )}°
            </div>


            <div class="day-min">
                ${Math.round(
                    d.temperature_2m_min[i]
                )}°
            </div>


            <div class="day-rain">

                ${rainIcon(rain)}
                ${rain}%

            </div>

        `;


        forecast.appendChild(card);
    }
}


/* ============================
   ΑΝΑΛΥΤΙΚΗ ΗΜΕΡΑΣ
============================ */

function showDay(index){

    selectedDay = index;

    renderDays();


    const d =
        weatherData.daily;

    const h =
        weatherData.hourly;


    let hourlyHTML = "";


    for(let i=0;i<h.time.length;i++){

        if(
            h.time[i].startsWith(
                d.time[index]
            )
        ){

            const time =
                new Date(
                    h.time[i]
                ).toLocaleTimeString(
                    "el-GR",
                    {
                        hour:"2-digit",
                        minute:"2-digit"
                    }
                );


            const isDay =
                h.is_day[i] === 1;


            const info =
                weatherInfo(
                    h.weather_code[i],
                    isDay
                );


            const temp =
                Math.round(
                    h.temperature_2m[i]
                );


            const feels =
                Math.round(
                    h.apparent_temperature[i]
                );


            const rain =
                h.precipitation_probability[i] ?? 0;


            const wind =
                Math.round(
                    h.wind_speed_10m[i] ?? 0
                );


            const direction =
                getWindDirection(
                    h.wind_direction_10m[i] ?? 0
                );


            hourlyHTML += `

                <div class="hour">

                    <div class="hour-time">
                        ${time}
                    </div>


                    <div class="hour-icon">
                        ${info[0]}
                    </div>


                    <div class="hour-temp">

                        🌡️ ${temp}°<br>

                        Αίσθηση ${feels}°

                    </div>


                    <div class="hour-rain">

                        Πιθανότητα υετού:<br>

                        ${rainIcon(rain)} ${rain}%

                    </div>


                    <div class="hour-wind">

                        💨 ${wind} km/h<br>

                        Διεύθυνση: ${direction}

                    </div>

                </div>

            `;
        }
    }


    const dailyInfo =
        weatherInfo(
            d.weather_code[index],
            true
        );


    const rain =
        d.precipitation_probability_max[index] ?? 0;


    document.getElementById("details").innerHTML = `

        <div class="details">


            <div class="details-header">

                <div class="details-title">

                    Πρόγνωση ανά ώρα —
                    ${
                        index === 0
                        ? "Σήμερα"
                        : getDayName(d.time[index])
                    }
                    ${getDate(d.time[index])}

                </div>


                <button
                    class="close-btn"
                    onclick="closeDetails()"
                >
                    ✕ Κλείσιμο
                </button>

            </div>


            <div class="hourly">

                ${hourlyHTML}

            </div>


        </div>

    `;
}


/* ============================
   ΚΛΕΙΣΙΜΟ
============================ */

function closeDetails(){

    document.getElementById("details").innerHTML = "";
}


/* ============================
   SEARCH BUTTON
============================ */

document
.getElementById("searchButton")
.addEventListener(
    "click",
    searchLocation
);


/* ============================
   ENTER
============================ */

document
.getElementById("searchInput")
.addEventListener(
    "keydown",
    function(event){

        if(event.key === "Enter"){
            searchLocation();
        }

    }
);


/* ============================
   ΑΡΧΙΚΑ ΘΕΣΣΑΛΟΝΙΚΗ
============================ */

loadWeather(
    40.6401,
    22.9444,
    "Θεσσαλονίκη",
    "Ελλάδα"
);

</script>

</body>
</html>
