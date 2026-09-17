<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<style>
*{
    box-sizing:border-box;
}

body{
    margin:0;
    font-family:Arial,Helvetica,sans-serif;
    background:#06284a;
    color:white;
}

.container{
    width:94%;
    max-width:1050px;
    margin:auto;
}

header{
    text-align:center;
    padding:28px 0 20px;
}

header h1{
    margin:0;
    font-size:34px;
}

header p{
    margin:8px 0 0;
    color:#c9dced;
    font-size:15px;
}

.search-box{
    display:flex;
    gap:10px;
    max-width:700px;
    margin:15px auto 25px;
}

.search-box input{
    flex:1;
    padding:14px 16px;
    border:none;
    border-radius:12px;
    font-size:16px;
    outline:none;
}

.search-box button{
    border:none;
    border-radius:12px;
    padding:0 22px;
    background:#1683d8;
    color:white;
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
}

#suggestions{
    max-width:700px;
    margin:-18px auto 20px;
    position:relative;
    z-index:20;
}

.suggestion{
    background:white;
    color:#17344e;
    padding:12px 15px;
    border-bottom:1px solid #ddd;
    cursor:pointer;
}

.suggestion:hover{
    background:#eaf5ff;
}

.location-name{
    text-align:center;
    font-size:27px;
    font-weight:bold;
    margin:10px 0 18px;
}

.current{
    background:#315575;
    border-radius:20px;
    padding:25px;
    display:flex;
    justify-content:space-between;
    align-items:center;
    gap:20px;
    box-shadow:0 8px 25px rgba(0,0,0,.18);
}

.current-left{
    display:flex;
    align-items:center;
    gap:18px;
}

.current-icon{
    font-size:65px;
    line-height:1;
}

.current-temp{
    font-size:52px;
    font-weight:bold;
}

.current-condition{
    font-size:18px;
    margin-top:5px;
    color:#dceaf5;
}

.current-right{
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:10px;
    min-width:300px;
}

.info{
    background:#416685;
    border-radius:12px;
    padding:12px;
    text-align:center;
}

.info-title{
    font-size:12px;
    color:#c9dced;
    margin-bottom:5px;
}

.info-value{
    font-size:16px;
    font-weight:bold;
}

.section-title{
    font-size:23px;
    margin:30px 0 15px;
}

.forecast{
    display:grid;
    grid-template-columns:repeat(5,1fr);
    gap:12px;
}

.day{
    background:#315575;
    border-radius:17px;
    padding:17px 10px;
    text-align:center;
    cursor:pointer;
    transition:.2s;
    border:2px solid transparent;
}

.day:hover{
    transform:translateY(-3px);
    background:#3a6385;
}

.day.selected{
    border-color:#55b8ff;
}

.day-name{
    font-size:16px;
    font-weight:bold;
}

.day-date{
    font-size:12px;
    color:#c8dbea;
    margin-top:3px;
}

.day-icon{
    font-size:40px;
    margin:13px 0 8px;
    min-height:45px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.temperatures{
    font-size:17px;
    font-weight:bold;
}

.min-temp{
    color:#c5d8e8;
    margin-left:5px;
}

.rain-prob{
    margin-top:8px;
    color:#bfe5ff;
    font-size:13px;
}

.hourly-container{
    margin-top:20px;
    padding-bottom:30px;
}

.selected-day-title{
    font-size:21px;
    margin:0 0 12px;
}

.hourly{
    display:flex;
    flex-direction:column;
    gap:8px;
}

.hour{
    background:#315575;
    border-radius:13px;
    padding:12px 15px;
    display:grid;
    grid-template-columns:75px 55px 1fr 110px 150px;
    align-items:center;
    gap:10px;
}

.hour-time{
    font-weight:bold;
}

.hour-icon{
    font-size:28px;
    text-align:center;
}

.hour-condition{
    color:#d9e8f3;
}

.hour-rain{
    color:#bfe5ff;
}

.hour-wind{
    color:#d9e8f3;
    text-align:right;
}

.loading{
    text-align:center;
    padding:25px;
    color:#cbddeb;
}

.error{
    background:#713f48;
    border-radius:12px;
    padding:15px;
    text-align:center;
    margin:15px 0;
}

.night-moon{
    color:#b9c0c8;
    font-size:1em;
}

.moon-cloud{
    display:flex;
    align-items:center;
    justify-content:center;
}

.moon-cloud .night-moon{
    margin-right:-5px;
    position:relative;
    z-index:1;
}

.moon-cloud .cloud{
    position:relative;
    z-index:2;
}

@media(max-width:800px){

    .forecast{
        grid-template-columns:repeat(3,1fr);
    }

    .current{
        flex-direction:column;
        text-align:center;
    }

    .current-right{
        width:100%;
        min-width:0;
    }

    .current-left{
        justify-content:center;
    }

    .hour{
        grid-template-columns:60px 45px 1fr;
    }

    .hour-rain,
    .hour-wind{
        grid-column:3;
        text-align:left;
    }
}

@media(max-width:500px){

    header h1{
        font-size:28px;
    }

    .search-box{
        flex-direction:column;
    }

    .search-box button{
        padding:13px;
    }

    .forecast{
        grid-template-columns:repeat(2,1fr);
    }

    .current-temp{
        font-size:45px;
    }

    .current-right{
        grid-template-columns:repeat(2,1fr);
    }
}
</style>
</head>

<body>

<div class="container">

<header>
    <h1>🌊 Greece Weather</h1>
    <p>Πρόγνωση καιρού για όλο τον κόσμο</p>
</header>

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

<div id="suggestions"></div>

<div id="locationName" class="location-name">
    Θεσσαλονίκη, Ελλάδα
</div>

<div id="currentWeather">
    <div class="loading">
        Φόρτωση καιρού...
    </div>
</div>

<h2 class="section-title">
    📅 Πρόγνωση 15 ημερών
</h2>

<div id="forecast" class="forecast">
    <div class="loading">
        Φόρτωση πρόγνωσης...
    </div>
</div>

<div class="hourly-container">

    <h2 id="selectedDayTitle" class="selected-day-title">
        Ωριαία πρόγνωση
    </h2>

    <div id="hourly" class="hourly">
        <div class="loading">
            Φόρτωση ωριαίας πρόγνωσης...
        </div>
    </div>

</div>

</div>


<script>

/* =====================================
   ΑΡΧΙΚΗ ΤΟΠΟΘΕΣΙΑ
===================================== */

let selectedLocation = {
    name:"Θεσσαλονίκη",
    country:"Ελλάδα",
    latitude:40.6401,
    longitude:22.9444
};

let weatherData = null;
let selectedDayIndex = 0;


/* =====================================
   ICONS
===================================== */

function weatherInfo(code,isDay,probability){

    code = Number(code) || 0;
    probability = Number(probability) || 0;

    /* Κάτω από 30%:
       ποτέ εικονίδιο υετού
    */

    if(probability < 30){

        if(code === 0){

            if(isDay){
                return {
                    icon:"☀️",
                    text:"Αίθριος"
                };
            }

            return {
                icon:'<span class="night-moon">☾</span>',
                text:"Αίθριος"
            };
        }

        if(code === 1){

            if(isDay){
                return {
                    icon:"🌤️",
                    text:"Κυρίως αίθριος"
                };
            }

            return {
                icon:'<span class="night-moon">☾</span>',
                text:"Κυρίως αίθριος"
            };
        }

        if(code === 2){

            if(isDay){
                return {
                    icon:"⛅",
                    text:"Λίγες νεφώσεις"
                };
            }

            return {
                icon:'<span class="moon-cloud"><span class="night-moon">☾</span><span class="cloud">☁️</span></span>',
                text:"Λίγες νεφώσεις"
            };
        }

        return {
            icon:"☁️",
            text:"Συννεφιά"
        };
    }


    /* Από 30% και πάνω
       κανονικά εικονίδια υετού
    */

    if(code === 0){

        return isDay
            ? {
                icon:"☀️",
                text:"Αίθριος"
            }
            : {
                icon:'<span class="night-moon">☾</span>',
                text:"Αίθριος"
            };
    }

    if(code === 1){

        return isDay
            ? {
                icon:"🌤️",
                text:"Κυρίως αίθριος"
            }
            : {
                icon:'<span class="night-moon">☾</span>',
                text:"Κυρίως αίθριος"
            };
    }

    if(code === 2){

        return isDay
            ? {
                icon:"⛅",
                text:"Λίγες νεφώσεις"
            }
            : {
                icon:'<span class="moon-cloud"><span class="night-moon">☾</span><span class="cloud">☁️</span></span>',
                text:"Λίγες νεφώσεις"
            };
    }

    if(code === 3)
        return {
            icon:"☁️",
            text:"Συννεφιά"
        };

    if(code === 45 || code === 48)
        return {
            icon:"🌫️",
            text:"Ομίχλη"
        };

    if(code >= 51 && code <= 57)
        return {
            icon:"🌦️",
            text:"Ψιλόβροχο"
        };

    if(code >= 61 && code <= 67)
        return {
            icon:"🌧️",
            text:"Βροχή"
        };

    if(code >= 71 && code <= 77)
        return {
            icon:"❄️",
            text:"Χιόνι"
        };

    if(code >= 80 && code <= 82)
        return {
            icon:"🌦️",
            text:"Μπόρες"
        };

    if(code === 85 || code === 86)
        return {
            icon:"🌨️",
            text:"Χιονομπόρες"
        };

    if(code >= 95)
        return {
            icon:"⛈️",
            text:"Καταιγίδα"
        };

    return {
        icon:"☁️",
        text:"Νεφελώδης"
    };
}


/* =====================================
   ΑΝΑΖΗΤΗΣΗ ΠΟΛΗΣ
===================================== */

const searchInput =
    document.getElementById("searchInput");

const suggestions =
    document.getElementById("suggestions");

const searchButton =
    document.getElementById("searchButton");


let searchTimeout = null;


searchInput.addEventListener("input",function(){

    clearTimeout(searchTimeout);

    const value =
        this.value.trim();

    if(value.length < 2){

        suggestions.innerHTML="";
        return;
    }

    searchTimeout =
        setTimeout(searchPlaces,350);
});


async function searchPlaces(){

    const value =
        searchInput.value.trim();

    if(value.length < 2)
        return;

    try{

        const url =
            "https://geocoding-api.open-meteo.com/v1/search" +
            "?name="+encodeURIComponent(value)+
            "&count=8"+
            "&language=el"+
            "&format=json";

        const response =
            await fetch(url);

        if(!response.ok)
            throw new Error("Geocoding error");

        const data =
            await response.json();

        suggestions.innerHTML="";

        if(!data.results || !data.results.length){

            suggestions.innerHTML =
                '<div class="suggestion">Δεν βρέθηκε τοποθεσία.</div>';

            return;
        }

        data.results.forEach(place=>{

            const item =
                document.createElement("div");

            item.className="suggestion";

            const parts=[];

            if(place.name)
                parts.push(place.name);

            if(place.admin1 &&
               place.admin1 !== place.name)
                parts.push(place.admin1);

            if(place.country)
                parts.push(place.country);

            item.textContent =
                parts.join(", ");


            item.addEventListener("click",function(){

                selectedLocation={
                    name:place.name,
                    country:place.country || "",
                    latitude:Number(place.latitude),
                    longitude:Number(place.longitude)
                };

                searchInput.value=place.name;

                suggestions.innerHTML="";

                loadWeather();
            });


            suggestions.appendChild(item);
        });

    }catch(error){

        console.error(error);

        suggestions.innerHTML =
            '<div class="suggestion">Σφάλμα αναζήτησης.</div>';
    }
}


searchButton.addEventListener(
    "click",
    searchPlaces
);


searchInput.addEventListener(
    "keydown",
    function(event){

        if(event.key==="Enter")
            searchPlaces();

    }
);


/* =====================================
   ΦΟΡΤΩΣΗ WEATHER
===================================== */

async function loadWeather(){

    const currentBox =
        document.getElementById("currentWeather");

    const forecastBox =
        document.getElementById("forecast");

    const hourlyBox =
        document.getElementById("hourly");


    currentBox.innerHTML =
        '<div class="loading">Φόρτωση καιρού...</div>';

    forecastBox.innerHTML =
        '<div class="loading">Φόρτωση πρόγνωσης...</div>';

    hourlyBox.innerHTML =
        '<div class="loading">Φόρτωση ωριαίας πρόγνωσης...</div>';


    document.getElementById("locationName")
        .textContent =
        selectedLocation.name+
        (selectedLocation.country
            ? ", "+selectedLocation.country
            : "");


    try{

        /*
         * Χρησιμοποιούμε απλή URL σύνταξη.
         * Το models=auto αφήνει την Open-Meteo
         * να επιλέξει τα κατάλληλα διαθέσιμα
         * μοντέλα για την τοποθεσία.
         */

        const url =
            "https://api.open-meteo.com/v1/forecast"+
            "?latitude="+encodeURIComponent(selectedLocation.latitude)+
            "&longitude="+encodeURIComponent(selectedLocation.longitude)+
            "&current="+encodeURIComponent(
                "temperature_2m,relative_humidity_2m,apparent_temperature,precipitation,weather_code,is_day,wind_speed_10m,wind_direction_10m"
            )+
            "&hourly="+encodeURIComponent(
                "temperature_2m,relative_humidity_2m,apparent_temperature,precipitation_probability,precipitation,rain,showers,snowfall,weather_code,cloud_cover,is_day,wind_speed_10m,wind_direction_10m"
            )+
            "&daily="+encodeURIComponent(
                "weather_code,temperature_2m_max,temperature_2m_min,apparent_temperature_max,apparent_temperature_min,precipitation_sum,precipitation_probability_max,wind_speed_10m_max,wind_direction_10m_dominant,sunrise,sunset"
            )+
            "&forecast_days=16"+
            "&timezone=auto"+
            "&temperature_unit=celsius"+
            "&wind_speed_unit=kmh"+
            "&precipitation_unit=mm"+
            "&models=auto"+
            "&cell_selection=land"+
            "&_="+Date.now();


        console.log("Weather URL:",url);


        const response =
            await fetch(
                url,
                {
                    method:"GET",
                    cache:"no-store"
                }
            );


        if(!response.ok){

            const errorText =
                await response.text();

            console.error(
                "Open-Meteo error:",
                response.status,
                errorText
            );

            throw new Error(
                "HTTP "+response.status
            );
        }


        const data =
            await response.json();


        console.log(
            "Weather data received:",
            data
        );


        if(
            !data ||
            !data.current ||
            !data.hourly ||
            !data.daily
        ){

            throw new Error(
                "Incomplete weather data"
            );
        }


        weatherData=data;

        selectedDayIndex=0;


        renderCurrent();

        renderForecast();

        renderHourly(0);


    }catch(error){

        console.error(
            "WEATHER ERROR:",
            error
        );


        currentBox.innerHTML =
            '<div class="error">'+
            'Δεν φορτώθηκαν τα δεδομένα καιρού.<br>'+
            '<small>Έλεγξε ότι ο κώδικας έχει αντικατασταθεί ολόκληρος.</small>'+
            '</div>';


        forecastBox.innerHTML="";

        hourlyBox.innerHTML="";
    }
}


/* =====================================
   CURRENT
===================================== */

function getCurrentProbability(){

    if(
        !weatherData ||
        !weatherData.hourly ||
        !weatherData.hourly.time
    )
        return 0;


    const now =
        Date.now();

    let bestIndex=0;

    let bestDifference=
        Infinity;


    for(
        let i=0;
        i<weatherData.hourly.time.length;
        i++
    ){

        const t =
            new Date(
                weatherData.hourly.time[i]
            ).getTime();

        const difference =
            Math.abs(t-now);


        if(difference < bestDifference){

            bestDifference=difference;

            bestIndex=i;
        }
    }


    return Number(
        weatherData.hourly
        .precipitation_probability[
            bestIndex
        ]
    ) || 0;
}


function renderCurrent(){

    const c =
        weatherData.current;


    const probability =
        getCurrentProbability();


    const info =
        weatherInfo(
            c.weather_code,
            Number(c.is_day)===1,
            probability
        );


    const windDirection =
        degreesToDirection(
            c.wind_direction_10m
        );


    document.getElementById(
        "currentWeather"
    ).innerHTML=`

        <div class="current">

            <div class="current-left">

                <div class="current-icon">
                    ${info.icon}
                </div>

                <div>

                    <div class="current-temp">
                        ${Math.round(Number(c.temperature_2m))}°C
                    </div>

                    <div class="current-condition">
                        ${info.text}
                    </div>

                </div>

            </div>


            <div class="current-right">

                <div class="info">
                    <div class="info-title">
                        Αίσθηση
                    </div>

                    <div class="info-value">
                        ${Math.round(Number(c.apparent_temperature))}°C
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        Υγρασία
                    </div>

                    <div class="info-value">
                        ${Number(c.relative_humidity_2m)}%
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        Άνεμος
                    </div>

                    <div class="info-value">
                        ${Math.round(Number(c.wind_speed_10m))} km/h
                    </div>
                </div>


                <div class="info">
                    <div class="info-title">
                        Κατεύθυνση
                    </div>

                    <div class="info-value">
                        ${windDirection}
                    </div>
                </div>

            </div>

        </div>
    `;
}


/* =====================================
   15 ΗΜΕΡΕΣ
===================================== */

function renderForecast(){

    const d =
        weatherData.daily;


    const box =
        document.getElementById(
            "forecast"
        );


    box.innerHTML="";


    const total =
        Math.min(
            15,
            d.time.length
        );


    for(
        let i=0;
        i<total;
        i++
    ){

        const date =
            new Date(
                d.time[i]+"T12:00:00"
            );


        const dayName =
            i===0
            ? "Σήμερα"
            : date.toLocaleDateString(
                "el-GR",
                {weekday:"short"}
            );


        const dateText =
            date.toLocaleDateString(
                "el-GR",
                {
                    day:"numeric",
                    month:"short"
                }
            );


        const probability =
            Number(
                d.precipitation_probability_max[i]
            ) || 0;


        const info =
            weatherInfo(
                d.weather_code[i],
                true,
                probability
            );


        const card =
            document.createElement("div");


        card.className =
            "day"+
            (
                i===selectedDayIndex
                ? " selected"
                : ""
            );


        card.innerHTML=`

            <div class="day-name">
                ${capitalize(dayName)}
            </div>

            <div class="day-date">
                ${dateText}
            </div>

            <div class="day-icon">
                ${info.icon}
            </div>

            <div class="temperatures">
                ${Math.round(Number(d.temperature_2m_max[i]))}°
                <span class="min-temp">
                    ${Math.round(Number(d.temperature_2m_min[i]))}°
                </span>
            </div>

            <div class="rain-prob">
                💧 ${probability}%
            </div>

        `;


        card.addEventListener(
            "click",
            function(){

                selectedDayIndex=i;


                document
                    .querySelectorAll(".day")
                    .forEach(
                        x=>x.classList.remove(
                            "selected"
                        )
                    );


                card.classList.add(
                    "selected"
                );


                renderHourly(i);
            }
        );


        box.appendChild(card);
    }
}


/* =====================================
   HOURLY
===================================== */

function renderHourly(dayIndex){

    const h =
        weatherData.hourly;

    const d =
        weatherData.daily;


    const targetDate =
        d.time[dayIndex];


    const box =
        document.getElementById(
            "hourly"
        );


    box.innerHTML="";


    const title =
        document.getElementById(
            "selectedDayTitle"
        );


    title.textContent =
        "Ωριαία πρόγνωση — "+
        new Date(
            targetDate+"T12:00:00"
        ).toLocaleDateString(
            "el-GR",
            {
                weekday:"long",
                day:"numeric",
                month:"long"
            }
        );


    let found=0;


    for(
        let i=0;
        i<h.time.length;
        i++
    ){

        /*
         * Τα timestamps της Open-Meteo
         * είναι ήδη στην timezone της τοποθεσίας
         * επειδή ζητήσαμε timezone=auto.
         */

        if(
            String(h.time[i]).substring(0,10)
            !== targetDate
        )
            continue;


        const timeString =
            String(h.time[i]).substring(11,16);


        const probability =
            Number(
                h.precipitation_probability[i]
            ) || 0;


        const info =
            weatherInfo(
                h.weather_code[i],
                Number(h.is_day[i])===1,
                probability
            );


        const direction =
            degreesToDirection(
                h.wind_direction_10m[i]
            );


        const row =
            document.createElement("div");


        row.className="hour";


        row.innerHTML=`

            <div class="hour-time">
                ${timeString}
            </div>

            <div class="hour-icon">
                ${info.icon}
            </div>

            <div class="hour-condition">
                ${Math.round(Number(h.temperature_2m[i]))}°C —
                ${info.text}
            </div>

            <div class="hour-rain">
                💧 ${probability}%
            </div>

            <div class="hour-wind">
                💨 ${Math.round(Number(h.wind_speed_10m[i]))} km/h
                ${direction}
            </div>

        `;


        box.appendChild(row);

        found++;
    }


    if(found===0){

        box.innerHTML =
            '<div class="loading">'+
            'Δεν υπάρχουν ωριαία δεδομένα για αυτή την ημέρα.'+
            '</div>';
    }
}


/* =====================================
   ΑΝΕΜΟΣ
===================================== */

function degreesToDirection(degrees){

    const n =
        Number(degrees);


    if(!Number.isFinite(n))
        return "";


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


    return directions[
        Math.round(n/45)%8
    ];
}


/* =====================================
   HELPERS
===================================== */

function capitalize(text){

    if(!text)
        return "";

    return text.charAt(0).toUpperCase()+
           text.slice(1);
}


/* =====================================
   ΑΡΧΙΚΗ ΦΟΡΤΩΣΗ
===================================== */

loadWeather();


/* =====================================
   ΑΝΑΝΕΩΣΗ ΚΑΘΕ 5 ΛΕΠΤΑ
===================================== */

setInterval(
    loadWeather,
    5*60*1000
);

</script>

</body>
</html>
