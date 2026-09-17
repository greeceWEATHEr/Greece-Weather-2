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
    background:
        linear-gradient(
            180deg,
            #022e55 0%,
            #012449 50%,
            #01172f 100%
        );
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
}

.subtitle{
    margin-top:5px;
    opacity:.8;
}


/* SEARCH */

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
    margin-top:5px;
    opacity:.8;
}


/* CURRENT */

.current{
    background:rgba(255,255,255,.10);
    border:1px solid rgba(255,255,255,.15);
    border-radius:24px;
    padding:25px;

    display:flex;
    justify-content:space-between;
    align-items:center;

    margin-bottom:25px;

    box-shadow:
        0 10px 35px rgba(0,0,0,.30);
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


/* TITLES */

.section-title{
    font-size:23px;
    font-weight:700;
    margin:12px 0 14px;
}


/* =========================
   15 ΗΜΕΡΕΣ
   4 - 4 - 4 - 3
========================= */

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

    box-shadow:
        0 8px 25px rgba(0,0,0,.35);
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


/* DETAILS */

.details{
    margin-top:25px;

    background:rgba(255,255,255,.10);

    border:1px solid rgba(255,255,255,.15);

    border-radius:24px;

    padding:25px;

    box-shadow:
        0 10px 35px rgba(0,0,0,.30);
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


/* INFO */

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


/* =========================
   ΩΡΙΑΙΑ
========================= */

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


/* LOADING */

.loading{
    text-align:center;
    padding:40px;
    font-size:18px;
}


/* ERROR */

.error{
    background:rgba(180,0,0,.25);

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
    opacity:.55;
    font-size:13px;
}


/* =========================
   TABLET / PC
========================= */

@media (min-width:601px){

    .forecast{
        grid-template-columns:repeat(4,1fr);
    }

}


/* =========================
   MOBILE
========================= */

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

<div class="logo">
🌤️ Greece Weather
</div>

<div class="subtitle">
15ήμερη πρόγνωση καιρού
</div>

</header>


<div class="search-area">

<div class="search-box">

<input
id="searchInput"
type="text"
placeholder="Αναζήτησε πόλη ή περιοχή..."
autocomplete="off"
>

<button id="searchButton">
Αναζήτηση
</button>

</div>

</div>


<div id="location" class="location"></div>


<div id="content">

<div class="loading">
⏳ Φόρτωση καιρού...
</div>

</div>


<footer>
Weather data powered by Open-Meteo
</footer>


</div>



<script>


let weatherData = null;

let selectedDay = 0;



/* =================================
   ΚΑΙΡΙΚΑ ΕΙΚΟΝΙΔΙΑ
================================= */

function weatherInfo(code,isDay){

    /*
       ΝΥΧΤΑ

       Δεν βάζουμε πάντα φεγγάρι.

       Το εικονίδιο εξαρτάται από
       τον πραγματικό κωδικό καιρού.
    */

    if(!isDay){

        if(code === 0){
            return ["🌙","Ξαστεριά"];
        }

        if(code === 1){
            return ["🌙","Κυρίως αίθριος"];
        }

        if(code === 2){
            return ["☁️","Λίγα σύννεφα"];
        }

        if(code === 3){
            return ["☁️","Συννεφιά"];
        }

        if(code === 45 || code === 48){
            return ["🌫️","Ομίχλη"];
        }

        if(code === 51 || code === 53 || code === 55){
            return ["🌧️","Ψιλή βροχή"];
        }

        if(
            code === 61 ||
            code === 63 ||
            code === 65 ||
            code === 66 ||
            code === 67
        ){
            return ["🌧️","Βροχή"];
        }

        if(
            code === 71 ||
            code === 73 ||
            code === 75 ||
            code === 77
        ){
            return ["🌨️","Χιόνι"];
        }

        if(
            code === 80 ||
            code === 81 ||
            code === 82
        ){
            return ["🌧️","Μπόρες"];
        }

        if(
            code === 85 ||
            code === 86
        ){
            return ["🌨️","Χιονομπόρες"];
        }

        if(code === 95){
            return ["⛈️","Καταιγίδα"];
        }

        if(code === 96 || code === 99){
            return ["⛈️","Καταιγίδα με χαλάζι"];
        }

        return ["☁️","Νυχτερινή συννεφιά"];
    }


    /* =================================
       ΗΜΕΡΑ
    ================================= */

    if(code === 0){
        return ["☀️","Αίθριος"];
    }

    if(code === 1){
        return ["🌤️","Κυρίως αίθριος"];
    }

    if(code === 2){
        return ["⛅","Μερική συννεφιά"];
    }

    if(code === 3){
        return ["☁️","Συννεφιά"];
    }

    if(code === 45 || code === 48){
        return ["🌫️","Ομίχλη"];
    }

    if(code === 51 || code === 53 || code === 55){
        return ["🌦️","Ψιλή βροχή"];
    }

    if(
        code === 61 ||
        code === 63 ||
        code === 65 ||
        code === 66 ||
        code === 67
    ){
        return ["🌧️","Βροχή"];
    }

    if(
        code === 71 ||
        code === 73 ||
        code === 75 ||
        code === 77
    ){
        return ["🌨️","Χιόνι"];
    }

    if(
        code === 80 ||
        code === 81 ||
        code === 82
    ){
        return ["🌦️","Μπόρες"];
    }

    if(
        code === 85 ||
        code === 86
    ){
        return ["🌨️","Χιονομπόρες"];
    }

    if(code === 95){
        return ["⛈️","Καταιγίδα"];
    }

    if(code === 96 || code === 99){
        return ["⛈️","Καταιγίδα με χαλάζι"];
    }

    return ["☁️","Μεταβλητός"];
}



/* =================================
   ΟΝΟΜΑ ΗΜΕΡΑΣ
================================= */

function getDayName(dateString){

    const names = [
        "Κυριακή",
        "Δευτέρα",
        "Τρίτη",
        "Τετάρτη",
        "Πέμπτη",
        "Παρασκευή",
        "Σάββατο"
    ];

    const date =
        new Date(dateString + "T12:00:00");

    return names[date.getDay()];
}



/* =================================
   ΗΜΕΡΟΜΗΝΙΑ
================================= */

function getDate(dateString){

    const date =
        new Date(dateString + "T12:00:00");

    return date.toLocaleDateString(
        "el-GR",
        {
            day:"2-digit",
            month:"2-digit"
        }
    );
}



/* =================================
   ΔΙΕΥΘΥΝΣΗ ΑΝΕΜΟΥ
================================= */

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

    const index =
        Math.round(degrees / 45) % 8;

    return directions[index];
}



/* =================================
   ΑΝΑΖΗΤΗΣΗ ΠΕΡΙΟΧΗΣ
================================= */

async function searchLocation(){

    const input =
        document.getElementById("searchInput");

    const query =
        input.value.trim();

    if(!query){
        return;
    }

    document.getElementById("content").innerHTML =
        '<div class="loading">🔎 Αναζήτηση περιοχής...</div>';

    try{

        const url =
            "https://geocoding-api.open-meteo.com/v1/search" +
            "?name=" +
            encodeURIComponent(query) +
            "&count=1" +
            "&language=el" +
            "&format=json";

        const response =
            await fetch(url);

        if(!response.ok){
            throw new Error("Geocoding error");
        }

        const data =
            await response.json();

        if(
            !data.results ||
            data.results.length === 0
        ){

            document.getElementById("content").innerHTML =
                '<div class="error">❌ Δεν βρέθηκε η περιοχή.</div>';

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
            '<div class="error">' +
            '❌ Δεν ήταν δυνατή η αναζήτηση.' +
            '</div>';
    }
}



/* =================================
   ΦΟΡΤΩΣΗ ΠΡΟΓΝΩΣΗΣ
================================= */

async function loadWeather(
    latitude,
    longitude,
    name,
    country
){

    document.getElementById("location").innerHTML =

        "<h1>📍 " +
        name +
        "</h1>" +

        "<p>" +
        country +
        "</p>";


    document.getElementById("content").innerHTML =
        '<div class="loading">🌦️ Φόρτωση πρόγνωσης...</div>';


    try{

        const url =

            "https://api.open-meteo.com/v1/forecast" +

            "?latitude=" +
            latitude +

            "&longitude=" +
            longitude +

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
            "wind_speed_10m," +
            "wind_direction_10m," +
            "is_day";


        const response =
            await fetch(url);


        if(!response.ok){
            throw new Error("Weather API error");
        }


        const data =
            await response.json();


        if(
            !data.daily ||
            !data.hourly ||
            !data.daily.time ||
            !data.hourly.time
        ){
            throw new Error("Incomplete data");
        }


        weatherData = data;

        selectedDay = 0;

        renderWeather();


    }catch(error){

        console.error(
            "WEATHER ERROR:",
            error
        );

        document.getElementById("content").innerHTML =
            '<div class="error">' +
            '❌ Δεν φορτώθηκαν τα δεδομένα καιρού.' +
            '<br><small>Δοκίμασε ξανά.</small>' +
            '</div>';
    }
}



/* =================================
   ΚΥΡΙΑ ΠΡΟΒΟΛΗ
================================= */

function renderWeather(){

    const d =
        weatherData.daily;


    const info =
        weatherInfo(
            d.weather_code[0],
            true
        );


    document.getElementById("content").innerHTML = `

        <div class="current">

            <div class="current-left">

                <div class="current-icon">
                    ${info[0]}
                </div>

                <div>

                    <div class="current-temp">
                        ${Math.round(
                            d.temperature_2m_max[0]
                        )}°
                    </div>

                    <div class="current-condition">
                        ${info[1]}
                    </div>

                </div>

            </div>


            <div class="current-right">

                <div>
                    🌡️ Ελάχιστη:
                    <b>
                    ${Math.round(
                        d.temperature_2m_min[0]
                    )}°C
                    </b>
                </div>

                <div>
                    💧 Βροχή:
                    <b>
                    ${d.precipitation_probability_max[0] ?? 0}%
                    </b>
                </div>

                <div>
                    💨 Άνεμος:
                    <b>
                    ${Math.round(
                        d.wind_speed_10m_max[0]
                    )} km/h
                    </b>
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



/* =================================
   15 ΚΟΥΤΑΚΙΑ
================================= */

function renderDays(){

    const d =
        weatherData.daily;


    const forecast =
        document.getElementById("forecast");


    forecast.innerHTML = "";


    for(let i=0;i<15;i++){

        /*
        Τα ημερήσια κουτάκια είναι
        ημερήσια πρόγνωση, οπότε
        χρησιμοποιούμε τον γενικό
        ημερήσιο καιρικό κωδικό.
        */

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


            <div class="day-temp">
                ${Math.round(
                    d.temperature_2m_max[i]
                )}°
            </div>


            <div class="day-min">
                ${Math.round(
                    d.temperature_2m_min[i]
                )}°
            </div>


            <div class="rain">
                💧 ${rain}%
            </div>

        `;


        forecast.appendChild(card);
    }
}



/* =================================
   ΑΝΑΛΥΤΙΚΗ ΗΜΕΡΑΣ
================================= */

function showDay(index){

    selectedDay = index;

    renderDays();


    const d =
        weatherData.daily;

    const h =
        weatherData.hourly;


    const info =
        weatherInfo(
            d.weather_code[index],
            true
        );


    const rainProbability =
        d.precipitation_probability_max[index] ?? 0;


    const rainAmount =
        d.precipitation_sum[index] ?? 0;


    const sunrise =
        new Date(
            d.sunrise[index]
        ).toLocaleTimeString(
            "el-GR",
            {
                hour:"2-digit",
                minute:"2-digit"
            }
        );


    const sunset =
        new Date(
            d.sunset[index]
        ).toLocaleTimeString(
            "el-GR",
            {
                hour:"2-digit",
                minute:"2-digit"
            }
        );


    /* =========================
       ΩΡΙΑΙΑ
    ========================= */

    let hourlyHTML = "";


    for(let i=0;i<h.time.length;i++){

        if(
            h.time[i].startsWith(
                d.time[index]
            )
        ){

            const hour =
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


            /*
            Εδώ χρησιμοποιούμε
            τον ΠΡΑΓΜΑΤΙΚΟ ωριαίο
            καιρικό κωδικό + is_day.

            Άρα τη νύχτα:
            καθαρός → 🌙
            σύννεφα → ☁️
            βροχή → 🌧️
            καταιγίδα → ⛈️
            χιόνι → 🌨️
            */

            const hourInfo =
                weatherInfo(
                    h.weather_code[i],
                    isDay
                );


            const windSpeed =
                Math.round(
                    h.wind_speed_10m[i] ?? 0
                );


            const degrees =
                h.wind_direction_10m[i] ?? 0;


            const direction =
                getWindDirection(
                    degrees
                );


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
                            h.temperature_2m[i]
                        )}°
                    </div>


                    <div class="hour-rain">
                        💧 ${
                            h.precipitation_probability[i]
                            ?? 0
                        }%
                    </div>


                    <div class="hour-wind">
                        💨 ${windSpeed} km/h
                    </div>


                    <div class="wind-direction">
                        ${direction}
                    </div>

                </div>

            `;
        }
    }


    /* =========================
       ΛΕΠΤΟΜΕΡΕΙΕΣ
    ========================= */

    document.getElementById("details").innerHTML = `

        <div class="details">


            <div class="details-title">

                ${
                    index === 0
                    ? "Σήμερα"
                    : getDayName(d.time[index])
                }

                · ${getDate(d.time[index])}

            </div>


            <div class="details-main">

                <div class="details-icon">
                    ${info[0]}
                </div>


                <div>

                    <div class="details-temperature">
                        ${Math.round(
                            d.temperature_2m_max[index]
                        )}°
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

                        ${Math.round(
                            d.temperature_2m_min[index]
                        )}°

                        —

                        ${Math.round(
                            d.temperature_2m_max[index]
                        )}°C

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
                        ${Math.round(
                            d.wind_speed_10m_max[index]
                        )} km/h
                    </div>

                </div>


                <div class="info">

                    <div class="info-title">
                        💨 Ριπές
                    </div>

                    <div class="info-value">
                        ${Math.round(
                            d.wind_gusts_10m_max[index]
                        )} km/h
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


            <div
                class="section-title"
                style="margin-top:28px"
            >
                Ωριαία πρόγνωση · άνεμος
            </div>


            <div class="hourly">

                ${hourlyHTML}

            </div>


        </div>

    `;
}



/* =================================
   ΑΝΑΖΗΤΗΣΗ ΜΕ ENTER
================================= */

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



/* =================================
   ΚΟΥΜΠΙ ΑΝΑΖΗΤΗΣΗΣ
================================= */

document
.getElementById("searchButton")
.addEventListener(
    "click",
    searchLocation
);



/* =================================
   ΑΡΧΙΚΗ ΠΕΡΙΟΧΗ
================================= */

loadWeather(
    40.6401,
    22.9444,
    "Θεσσαλονίκη",
    "Ελλάδα"
);

</script>

</body>
</html>
