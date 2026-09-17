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
    margin:15px auto 25px;
    max-width:700px;
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

.search-box button:hover{
    background:#2196ed;
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

.suggestion:first-child{
    border-radius:10px 10px 0 0;
}

.suggestion:last-child{
    border-radius:0 0 10px 10px;
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
    gap:0;
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

    .hour{
        grid-template-columns:55px 45px 1fr;
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
    <button onclick="searchLocation()">Αναζήτηση</button>
</div>

<div id="suggestions"></div>

<div id="locationName" class="location-name">Θεσσαλονίκη, Ελλάδα</div>

<div id="currentWeather">
    <div class="loading">Φόρτωση καιρού...</div>
</div>

<h2 class="section-title">📅 Πρόγνωση 15 ημερών</h2>

<div id="forecast" class="forecast">
    <div class="loading">Φόρτωση πρόγνωσης...</div>
</div>

<div class="hourly-container">
    <h2 id="selectedDayTitle" class="selected-day-title">
        Ωριαία πρόγνωση
    </h2>

    <div id="hourly" class="hourly">
        <div class="loading">Φόρτωση ωριαίας πρόγνωσης...</div>
    </div>
</div>

</div>

<script>

let weatherData = null;

let selectedLocation = {
    name:"Thessaloniki",
    latitude:40.6401,
    longitude:22.9444,
    country:"Greece"
};

let selectedDayIndex = 0;


/* =========================
   WEATHER ICONS
========================= */

function weatherInfo(code,isDay,probability){

    /*
      Κάτω από 30% πιθανότητα υετού:
      ΔΕΝ εμφανίζουμε βροχή/χιόνι/καταιγίδα.
    */

    if(probability !== null && probability < 30){

        if(isDay){

            if(code === 0)
                return {icon:"☀️",text:"Αίθριος"};

            if(code === 1)
                return {icon:"🌤️",text:"Κυρίως αίθριος"};

            if(code === 2)
                return {icon:"⛅",text:"Λίγες νεφώσεις"};

            return {icon:"☁️",text:"Νεφελώδης"};
        }

        if(code === 0)
            return {
                icon:'<span class="night-moon">☾</span>',
                text:"Αίθριος"
            };

        if(code === 1)
            return {
                icon:'<span class="night-moon">☾</span>',
                text:"Κυρίως αίθριος"
            };

        if(code === 2)
            return {
                icon:'<span class="moon-cloud"><span class="night-moon">☾</span><span class="cloud">☁️</span></span>',
                text:"Λίγες νεφώσεις"
            };

        return {
            icon:"☁️",
            text:"Νεφελώδης"
        };
    }


    /* Κανονική πρόγνωση */

    if(code === 0){
        if(isDay)
            return {icon:"☀️",text:"Αίθριος"};

        return {
            icon:'<span class="night-moon">☾</span>',
            text:"Αίθριος"
        };
    }

    if(code === 1){
        if(isDay)
            return {icon:"🌤️",text:"Κυρίως αίθριος"};

        return {
            icon:'<span class="night-moon">☾</span>',
            text:"Κυρίως αίθριος"
        };
    }

    if(code === 2){
        if(isDay)
            return {icon:"⛅",text:"Λίγες νεφώσεις"};

        return {
            icon:'<span class="moon-cloud"><span class="night-moon">☾</span><span class="cloud">☁️</span></span>',
            text:"Λίγες νεφώσεις"
        };
    }

    if(code === 3)
        return {icon:"☁️",text:"Συννεφιά"};

    if(code === 45 || code === 48)
        return {icon:"🌫️",text:"Ομίχλη"};

    if(code >= 51 && code <= 57)
        return {icon:"🌦️",text:"Ψιλόβροχο"};

    if(code >= 61 && code <= 67)
        return {icon:"🌧️",text:"Βροχή"};

    if(code === 71 || code === 73 || code === 75 || code === 77)
        return {icon:"❄️",text:"Χιόνι"};

    if(code >= 80 && code <= 82)
        return {icon:"🌦️",text:"Μπόρες"};

    if(code === 85 || code === 86)
        return {icon:"🌨️",text:"Χιονομπόρες"};

    if(code >= 95)
        return {icon:"⛈️",text:"Καταιγίδα"};

    return isDay
        ? {icon:"⛅",text:"Μεταβλητός καιρός"}
        : {
            icon:'<span class="night-moon">☾</span>',
            text:"Μεταβλητός καιρός"
        };
}


/* =========================
   SEARCH
========================= */

const searchInput = document.getElementById("searchInput");
const suggestions = document.getElementById("suggestions");

let searchTimer;

searchInput.addEventListener("input",function(){

    clearTimeout(searchTimer);

    const value = this.value.trim();

    if(value.length < 2){
        suggestions.innerHTML="";
        return;
    }

    searchTimer=setTimeout(async()=>{

        try{

            const url =
                "https://geocoding-api.open-meteo.com/v1/search" +
                "?name="+encodeURIComponent(value)+
                "&count=10"+
                "&language=el"+
                "&format=json";

            const response=await fetch(url);

            if(!response.ok)
                throw new Error("Search error");

            const data=await response.json();

            suggestions.innerHTML="";

            if(!data.results || data.results.length===0){

                suggestions.innerHTML=
                    '<div class="suggestion">Δεν βρέθηκε τοποθεσία</div>';

                return;
            }

            data.results.forEach(place=>{

                const div=document.createElement("div");

                div.className="suggestion";

                div.textContent=
                    `${place.name}, ${place.country || ""}` +
                    (place.admin1 ? ` — ${place.admin1}` : "");

                div.onclick=()=>{

                    selectedLocation={
                        name:place.name,
                        latitude:place.latitude,
                        longitude:place.longitude,
                        country:place.country || ""
                    };

                    searchInput.value=place.name;
                    suggestions.innerHTML="";

                    loadWeather();
                };

                suggestions.appendChild(div);
            });

        }catch(error){

            suggestions.innerHTML=
                '<div class="suggestion">Σφάλμα αναζήτησης</div>';
        }

    },300);
});


function searchLocation(){

    const firstSuggestion=suggestions.querySelector(".suggestion");

    if(firstSuggestion)
        firstSuggestion.click();
}


/* =========================
   LOAD WEATHER
========================= */

async function loadWeather(){

    document.getElementById("locationName").textContent =
        `${selectedLocation.name}, ${selectedLocation.country}`;

    document.getElementById("currentWeather").innerHTML =
        '<div class="loading">Φόρτωση καιρού...</div>';

    document.getElementById("forecast").innerHTML =
        '<div class="loading">Φόρτωση πρόγνωσης...</div>';

    document.getElementById("hourly").innerHTML =
        '<div class="loading">Φόρτωση ωριαίας πρόγνωσης...</div>';

    try{

        const params = new URLSearchParams({

            latitude:selectedLocation.latitude,
            longitude:selectedLocation.longitude,

            current:
                "temperature_2m,"+
                "relative_humidity_2m,"+
                "apparent_temperature,"+
                "precipitation,"+
                "weather_code,"+
                "is_day,"+
                "wind_speed_10m,"+
                "wind_direction_10m",

            hourly:
                "temperature_2m,"+
                "relative_humidity_2m,"+
                "apparent_temperature,"+
                "precipitation_probability,"+
                "precipitation,"+
                "rain,"+
                "showers,"+
                "snowfall,"+
                "weather_code,"+
                "cloud_cover,"+
                "is_day,"+
                "wind_speed_10m,"+
                "wind_direction_10m",

            daily:
                "weather_code,"+
                "temperature_2m_max,"+
                "temperature_2m_min,"+
                "apparent_temperature_max,"+
                "apparent_temperature_min,"+
                "precipitation_sum,"+
                "precipitation_probability_max,"+
                "wind_speed_10m_max,"+
                "wind_direction_10m_dominant,"+
                "sunrise,"+
                "sunset",

            forecast_days:"16",

            timezone:"auto",

            temperature_unit:"celsius",

            wind_speed_unit:"kmh",

            precipitation_unit:"mm",

            models:"auto",

            cell_selection:"land",

            _ : Date.now()
        });


        const url =
            "https://api.open-meteo.com/v1/forecast?"+
            params.toString();


        const response=await fetch(url,{
            cache:"no-store"
        });


        if(!response.ok)
            throw new Error("Weather request failed");


        weatherData=await response.json();

        renderCurrent();
        renderForecast();

        selectedDayIndex=0;
        renderHourly(0);

    }catch(error){

        console.error(error);

        document.getElementById("currentWeather").innerHTML=
            '<div class="error">Δεν ήταν δυνατή η φόρτωση των δεδομένων καιρού.</div>';

        document.getElementById("forecast").innerHTML="";

        document.getElementById("hourly").innerHTML="";
    }
}


/* =========================
   CURRENT WEATHER
========================= */

function getCurrentProbability(){

    if(!weatherData || !weatherData.hourly)
        return 0;

    const now=new Date();

    let bestIndex=0;
    let bestDifference=Infinity;

    weatherData.hourly.time.forEach((time,index)=>{

        const difference=
            Math.abs(new Date(time)-now);

        if(difference<bestDifference){

            bestDifference=difference;
            bestIndex=index;
        }
    });

    return weatherData.hourly.precipitation_probability[bestIndex] ?? 0;
}


function renderCurrent(){

    const c=weatherData.current;

    const probability=getCurrentProbability();

    const info=weatherInfo(
        c.weather_code,
        c.is_day===1,
        probability
    );

    const windDirection=degreesToDirection(c.wind_direction_10m);

    document.getElementById("currentWeather").innerHTML=`

        <div class="current">

            <div class="current-left">

                <div class="current-icon">
                    ${info.icon}
                </div>

                <div>

                    <div class="current-temp">
                        ${Math.round(c.temperature_2m)}°C
                    </div>

                    <div class="current-condition">
                        ${info.text}
                    </div>

                </div>

            </div>


            <div class="current-right">

                <div class="info">
                    <div class="info-title">Αίσθηση</div>
                    <div class="info-value">
                        ${Math.round(c.apparent_temperature)}°C
                    </div>
                </div>

                <div class="info">
                    <div class="info-title">Υγρασία</div>
                    <div class="info-value">
                        ${c.relative_humidity_2m}%
                    </div>
                </div>

                <div class="info">
                    <div class="info-title">Άνεμος</div>
                    <div class="info-value">
                        ${Math.round(c.wind_speed_10m)} km/h
                    </div>
                </div>

                <div class="info">
                    <div class="info-title">Κατεύθυνση</div>
                    <div class="info-value">
                        ${windDirection}
                    </div>
                </div>

            </div>

        </div>
    `;
}


/* =========================
   15 DAY FORECAST
========================= */

function renderForecast(){

    const d=weatherData.daily;

    const container=document.getElementById("forecast");

    container.innerHTML="";

    const numberOfDays=Math.min(15,d.time.length);


    for(let i=0;i<numberOfDays;i++){

        const date=new Date(d.time[i]+"T12:00:00");

        const dayName=
            i===0
            ? "Σήμερα"
            : date.toLocaleDateString("el-GR",{
                weekday:"short"
            });

        const dateText=
            date.toLocaleDateString("el-GR",{
                day:"numeric",
                month:"short"
            });


        const probability=
            d.precipitation_probability_max[i] ?? 0;


        const isDay=true;


        const info=weatherInfo(
            d.weather_code[i],
            isDay,
            probability
        );


        const card=document.createElement("div");

        card.className=
            "day"+
            (i===selectedDayIndex ? " selected":"");


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

                ${Math.round(d.temperature_2m_max[i])}°

                <span class="min-temp">
                    ${Math.round(d.temperature_2m_min[i])}°
                </span>

            </div>

            <div class="rain-prob">
                💧 ${probability}%
            </div>
        `;


        card.onclick=()=>{

            selectedDayIndex=i;

            document
                .querySelectorAll(".day")
                .forEach(x=>x.classList.remove("selected"));

            card.classList.add("selected");

            renderHourly(i);

            document
                .getElementById("selectedDayTitle")
                .scrollIntoView({
                    behavior:"smooth",
                    block:"start"
                });
        };


        container.appendChild(card);
    }
}


/* =========================
   HOURLY
========================= */

function renderHourly(dayIndex){

    const h=weatherData.hourly;
    const d=weatherData.daily;

    const targetDate=d.time[dayIndex];

    const container=document.getElementById("hourly");

    container.innerHTML="";


    document.getElementById("selectedDayTitle").textContent=
        "Ωριαία πρόγνωση — "+
        new Date(targetDate+"T12:00:00")
        .toLocaleDateString("el-GR",{
            weekday:"long",
            day:"numeric",
            month:"long"
        });


    let count=0;


    for(let i=0;i<h.time.length;i++){

        if(h.time[i].startsWith(targetDate)){

            const date=new Date(h.time[i]);

            const hour=
                date.toLocaleTimeString("el-GR",{
                    hour:"2-digit",
                    minute:"2-digit"
                });


            const probability=
                h.precipitation_probability[i] ?? 0;


            const info=weatherInfo(
                h.weather_code[i],
                h.is_day[i]===1,
                probability
            );


            const windDirection=
                degreesToDirection(
                    h.wind_direction_10m[i]
                );


            const row=document.createElement("div");

            row.className="hour";


            row.innerHTML=`

                <div class="hour-time">
                    ${hour}
                </div>

                <div class="hour-icon">
                    ${info.icon}
                </div>

                <div class="hour-condition">
                    ${Math.round(h.temperature_2m[i])}°C —
                    ${info.text}
                </div>

                <div class="hour-rain">
                    💧 ${probability}%
                </div>

                <div class="hour-wind">
                    💨 ${Math.round(h.wind_speed_10m[i])} km/h
                    ${windDirection}
                </div>

            `;


            container.appendChild(row);

            count++;
        }
    }


    if(count===0){

        container.innerHTML=
            '<div class="loading">Δεν υπάρχουν ωριαία δεδομένα.</div>';
    }
}


/* =========================
   WIND DIRECTION
========================= */

function degreesToDirection(degrees){

    if(degrees===null || degrees===undefined)
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

    const index=
        Math.round(degrees/45)%8;

    return directions[index];
}


/* =========================
   HELPERS
========================= */

function capitalize(text){

    if(!text)
        return "";

    return text.charAt(0).toUpperCase()+text.slice(1);
}


/* =========================
   INITIAL LOAD
========================= */

loadWeather();


/*
   Αυτόματη ανανέωση δεδομένων
   κάθε 5 λεπτά.
*/

setInterval(()=>{

    loadWeather();

},5*60*1000);


/*
   Enter στην αναζήτηση
*/

searchInput.addEventListener("keydown",function(event){

    if(event.key==="Enter")
        searchLocation();

});

</script>

</body>
</html>
