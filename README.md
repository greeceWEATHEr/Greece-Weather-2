<!DOCTYPE html>
<html lang="el">

<head>

<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<style>

*{
    box-sizing:border-box;
}

body{
    margin:0;
    font-family:Arial,Helvetica,sans-serif;
    color:#fff;

    background:
        linear-gradient(
            180deg,
            #071d35,
            #0d3762
        );
}

.container{
    width:min(100%,960px);
    margin:auto;
    padding:16px;
}


/* =====================================
   HEADER
===================================== */

.header{
    background:rgba(3,20,38,.72);
    padding:28px 20px;
    text-align:center;
    margin-bottom:25px;
}

.header h1{
    margin:0;
    font-size:30px;
}

.header p{
    margin:18px 0 0;
    color:#d6dce4;
    font-size:16px;
}


/* =====================================
   SEARCH
===================================== */

.search{
    display:flex;
    gap:10px;
    margin-bottom:25px;
}

.search input{
    flex:1;
    border:0;
    outline:0;
    border-radius:15px;
    padding:17px;
    font-size:16px;
}

.search button{
    border:0;
    border-radius:15px;
    padding:0 22px;
    font-weight:bold;
    font-size:15px;
    cursor:pointer;
}


/* =====================================
   CURRENT
===================================== */

.current{
    background:rgba(57,85,117,.72);
    border-radius:20px;
    padding:25px;
    text-align:center;
    margin-bottom:25px;
}

.current h2{
    margin:0 0 20px;
    font-size:26px;
}

.temperature{
    font-size:60px;
    font-weight:300;
    margin-bottom:15px;
}

.condition{
    font-size:17px;
    margin-bottom:24px;
}

.current-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:12px;
}

.current-box{
    background:rgba(104,133,165,.48);
    border-radius:14px;
    padding:16px 8px;
}

.current-box span{
    display:block;
    color:#e0e5ea;
    margin-bottom:5px;
}

.current-box strong{
    font-size:15px;
}


/* =====================================
   SECTION TITLE
===================================== */

.section-title{
    display:flex;
    align-items:center;
    gap:8px;

    font-size:24px;
    font-weight:bold;

    border-bottom:
        2px solid
        rgba(255,255,255,.55);

    padding-bottom:12px;
    margin-bottom:15px;
}


/* =====================================
   DAILY
===================================== */

.forecast{
    display:grid;
    grid-template-columns:repeat(6,1fr);
    gap:12px;
}

.day{
    background:rgba(53,84,119,.78);

    border-radius:17px;

    padding:18px 8px;

    text-align:center;

    cursor:pointer;

    transition:.18s;

    border:
        1px solid
        transparent;

    min-height:195px;
}

.day:hover{
    transform:translateY(-3px);

    background:
        rgba(72,105,143,.95);

    border-color:
        rgba(255,255,255,.25);
}

.day:active{
    transform:scale(.97);
}

.day-name{
    font-weight:bold;
    font-size:15px;
}

.date{
    margin-top:9px;
    color:#e1e5e9;
    font-size:14px;
}

.icon{
    font-size:35px;
    margin:18px 0 12px;

    height:42px;

    display:flex;
    align-items:center;
    justify-content:center;
}

.temperatures{
    display:flex;
    flex-direction:column;
    align-items:center;
    gap:3px;
}

.max{
    font-size:18px;
    font-weight:bold;
}

.min{
    margin-top:0;
    color:#d0d7df;
    font-size:15px;
}

.rain{
    margin-top:10px;
    font-size:12px;
    color:#c9e9ff;
}


/* =====================================
   NIGHT MOON
===================================== */

.night-moon{
    display:inline-block;

    filter:
        grayscale(1)
        brightness(.78)
        sepia(.08)
        hue-rotate(175deg);

    opacity:.90;
}


/* =====================================
   NIGHT WEATHER ICONS
===================================== */

.night-partly-cloudy,
.night-rain,
.night-snow,
.night-sleet,
.night-storm{

    width:42px;
    height:42px;

    display:inline-block;

    background-position:center;
    background-repeat:no-repeat;
    background-size:contain;
}


/* NIGHT PARTLY CLOUDY */

.night-partly-cloudy{

    background-image:url(
        "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='25' cy='23' r='15' fill='%2393a8bd'/%3E%3Cpath d='M14 44c0-7 5.7-12.7 12.7-12.7 4.7 0 8.8 2.5 11 6.3 1.1-.4 2.3-.6 3.6-.6 6.5 0 11.7 5.2 11.7 11.7H14.7C14.2 47.3 14 45.7 14 44z' fill='%23cbd3dc'/%3E%3C/svg%3E"
    );

}


/* NIGHT RAIN */

.night-rain{

    background-image:url(
        "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='24' cy='21' r='14' fill='%2393a8bd'/%3E%3Cpath d='M13 40c0-6.8 5.5-12.3 12.3-12.3 4.5 0 8.5 2.4 10.6 6 1-.4 2.2-.6 3.4-.6 6.2 0 11.2 5 11.2 11.2H13.6C13.2 43 13 41.5 13 40z' fill='%23cbd3dc'/%3E%3Cpath d='M27 47l-3 7M37 47l-3 7M47 47l-3 7' stroke='%237eb5d8' stroke-width='3' stroke-linecap='round'/%3E%3C/svg%3E"
    );

}


/* NIGHT SNOW */

.night-snow{

    background-image:url(
        "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='24' cy='21' r='14' fill='%2393a8bd'/%3E%3Cpath d='M13 40c0-6.8 5.5-12.3 12.3-12.3 4.5 0 8.5 2.4 10.6 6 1-.4 2.2-.6 3.4-.6 6.2 0 11.2 5 11.2 11.2H13.6C13.2 43 13 41.5 13 40z' fill='%23cbd3dc'/%3E%3Ctext x='21' y='58' font-size='12' fill='%23e8f3ff'%3E❄%3C/text%3E%3Ctext x='37' y='58' font-size='12' fill='%23e8f3ff'%3E❄%3C/text%3E%3C/svg%3E"
    );

}


/* NIGHT SLEET */

.night-sleet{

    background-image:url(
        "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='24' cy='21' r='14' fill='%2393a8bd'/%3E%3Cpath d='M13 40c0-6.8 5.5-12.3 12.3-12.3 4.5 0 8.5 2.4 10.6 6 1-.4 2.2-.6 3.4-.6 6.2 0 11.2 5 11.2 11.2H13.6C13.2 43 13 41.5 13 40z' fill='%23cbd3dc'/%3E%3Cpath d='M24 47l-3 7M35 47l-3 7' stroke='%237eb5d8' stroke-width='3' stroke-linecap='round'/%3E%3Cpath d='M45 48l4 4M49 48l-4 4M47 46v8M43 50h8' stroke='%23e8f3ff' stroke-width='1.8' stroke-linecap='round'/%3E%3C/svg%3E"
    );

}


/* NIGHT STORM */

.night-storm{

    background-image:url(
        "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='23' cy='20' r='14' fill='%2393a8bd'/%3E%3Cpath d='M12 40c0-7 5.7-12.7 12.7-12.7 4.6 0 8.7 2.5 10.8 6.2 1-.4 2.2-.6 3.4-.6 6.4 0 11.6 5.2 11.6 11.6H12.7C12.3 43 12 41.5 12 40z' fill='%23aeb9c5'/%3E%3Cpath d='M34 40l-7 12h7l-3 9 11-15h-7l5-6z' fill='%23e5d77a'/%3E%3C/svg%3E"
    );

}


/* =====================================
   HOURLY
===================================== */

.hourly-section{
    display:none;

    margin-top:28px;

    background:
        rgba(5,27,50,.72);

    border-radius:20px;

    padding:20px;
}

.hourly-header{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:10px;

    border-bottom:
        1px solid
        rgba(255,255,255,.3);

    padding-bottom:15px;
    margin-bottom:15px;
}

.hourly-header h3{
    margin:0;
    font-size:21px;
}

.close-hourly{
    background:
        rgba(255,255,255,.15);

    border:0;
    color:white;

    border-radius:10px;

    padding:8px 13px;

    cursor:pointer;
}


/* =====================================
   HOURLY VERTICAL
===================================== */

.hourly{
    display:grid;
    gap:8px;
}

.hour{
    display:grid;

    grid-template-columns:
        65px
        55px
        115px
        minmax(180px,1fr)
        80px
        120px;

    align-items:center;

    background:
        rgba(65,96,130,.62);

    border-radius:12px;

    padding:12px 10px;

    gap:10px;
}

.hour-time{
    font-weight:bold;
    font-size:15px;
}

.hour-icon{
    font-size:25px;
    text-align:center;

    height:38px;

    display:flex;
    align-items:center;
    justify-content:center;
}

.hour-data{
    font-size:13px;
    color:#e4e8ed;
    line-height:1.5;
}

.precipitation{
    display:flex;
    align-items:center;
    gap:5px;
    flex-wrap:wrap;
}

.precipitation b{
    color:#fff;
}

.precipitation-none{
    color:#d5dce4;
}

.intensity{
    font-weight:bold;
}


/* =====================================
   MODEL INFO
===================================== */

.model-info{
    margin-top:18px;

    color:#bdc9d6;

    font-size:12px;

    line-height:1.5;
}


/* =====================================
   LOADING
===================================== */

.loading{
    text-align:center;
    padding:30px;
    font-size:16px;
}


/* =====================================
   RESPONSIVE
===================================== */

@media(max-width:850px){

    .forecast{
        grid-template-columns:repeat(3,1fr);
    }

    .hour{
        grid-template-columns:
            55px
            45px
            95px
            1fr;
    }

    .hour-data:nth-child(5),
    .hour-data:nth-child(6){
        display:none;
    }

}


@media(max-width:600px){

    .current-grid{
        grid-template-columns:1fr;
    }

    .forecast{
        grid-template-columns:repeat(3,1fr);
        gap:9px;
    }

    .day{
        padding:15px 5px;
    }

    .icon{
        font-size:30px;
    }

    .hour{
        grid-template-columns:
            50px
            42px
            1fr;
        gap:7px;
        padding:11px 8px;
    }

    .hour-data:nth-child(4){
        grid-column:3;
    }

}


@media(max-width:430px){

    .container{
        padding:12px;
    }

    .header h1{
        font-size:26px;
    }

    .temperature{
        font-size:52px;
    }

    .forecast{
        grid-template-columns:repeat(3,1fr);
        gap:7px;
    }

    .day{
        min-height:185px;
        padding:14px 3px;
    }

    .day-name{
        font-size:14px;
    }

    .date{
        font-size:12px;
    }

    .max{
        font-size:17px;
    }

    .min{
        font-size:14px;
    }

    .rain{
        font-size:11px;
    }

    .hourly-section{
        padding:12px;
    }

    .hourly-header h3{
        font-size:17px;
    }

    .close-hourly{
        padding:7px 9px;
        font-size:12px;
    }

}

</style>

</head>


<body>

<div class="container">


<div class="header">

    <h1>
        🇬🇷 Greece Weather
    </h1>

    <p>
        Πρόγνωση καιρού για όλη την Ελλάδα
    </p>

</div>


<div class="search">

    <input
        id="cityInput"
        placeholder="Γράψε πόλη..."
        value="Θεσσαλονίκη"
    >

    <button onclick="searchCity()">
        Αναζήτηση
    </button>

</div>


<div id="current"></div>


<div class="section-title">
    📅 Πρόγνωση 15 ημερών
</div>


<div id="forecast" class="forecast">

    <div class="loading">
        Φόρτωση πρόγνωσης...
    </div>

</div>


<div id="hourlySection" class="hourly-section">

    <div class="hourly-header">

        <h3 id="hourlyTitle"></h3>

        <button
            class="close-hourly"
            onclick="closeHourly()">

            ✕ Κλείσιμο

        </button>

    </div>


    <div id="hourly" class="hourly"></div>

</div>


<div class="model-info">

    ECMWF IFS HRES • NOAA GFS • DWD ICON

    <br>

    Αυτόματη ανανέωση δεδομένων κάθε 5 λεπτά,
    συγχρονισμένη στα 00, 05, 10, 15, 20, 25...
    λεπτά της ώρας.

    <br>

    Η συχνότητα νέων runs των μοντέλων
    εξαρτάται από τον εκάστοτε κύκλο έκδοσής τους.

</div>


</div>


<script>

/* =====================================
   GLOBAL
===================================== */

let weatherData = null;

let locationData = null;

let lastCity = "";

let selectedDayIndex = null;


/* =====================================
   WEATHER INTENSITY
===================================== */

function precipitationIntensity(probability, amount){

    const p = Number(probability || 0);
    const mm = Number(amount || 0);

    if(p < 30)
        return "";

    /*
       Η ένταση χρησιμοποιεί και την
       πιθανότητα και την πραγματική
       ποσότητα υετού.
    */

    if(p >= 85 || mm >= 10)
        return "ισχυρή";

    if(p >= 70 || mm >= 5)
        return "μέτρια προς ισχυρή";

    if(p >= 50 || mm >= 2)
        return "μέτρια";

    return "ασθενής";
}


/* =====================================
   WEATHER ICON
===================================== */

function weatherIcon(
    code,
    isDay = true,
    precipitationProbability = 0
){

    const precipOK =
        Number(precipitationProbability || 0) >= 30;


    /*
       Κάτω από 30% δεν εμφανίζουμε
       φαινόμενο υετού.
    */

    if(!precipOK){

        if(code === 0){

            if(isDay)
                return "☀️";

            return '<span class="night-moon">🌙</span>';

        }

        if(code === 1){

            if(isDay)
                return "🌤️";

            return '<span class="night-moon">🌙</span>';

        }

        if(code === 2){

            if(isDay)
                return "🌤️";

            return `
                <span
                    class="night-partly-cloudy"
                    aria-label="Λίγες νεφώσεις">
                </span>
            `;

        }

        return "☁️";
    }


    /* ΚΑΘΑΡΟΣ */

    if(code === 0){

        if(isDay)
            return "☀️";

        return '<span class="night-moon">🌙</span>';
    }


    /* ΚΥΡΙΩΣ ΑΙΘΡΙΟΣ */

    if(code === 1){

        if(isDay)
            return "🌤️";

        return '<span class="night-moon">🌙</span>';
    }


    /* ΛΙΓΕΣ ΝΕΦΩΣΕΙΣ */

    if(code === 2){

        if(isDay)
            return "🌤️";

        return `
            <span
                class="night-partly-cloudy"
                aria-label="Λίγες νεφώσεις τη νύχτα">
            </span>
        `;
    }


    /* ΣΥΝΝΕΦΙΑ */

    if(code === 3)
        return "☁️";


    /* ΟΜΙΧΛΗ */

    if([45,48].includes(code))
        return "🌫️";


    /* ΨΙΛΟΒΡΟΧΟ */

    if([51,53,55,56,57].includes(code)){

        if(isDay)
            return "🌧️";

        return `
            <span
                class="night-rain"
                aria-label="Νυχτερινό ψιλόβροχο">
            </span>
        `;
    }


    /* ΒΡΟΧΗ / ΜΠΟΡΕΣ */

    if([61,63,65,80,81,82].includes(code)){

        if(isDay)
            return "🌧️";

        return `
            <span
                class="night-rain"
                aria-label="Νυχτερινή βροχή">
            </span>
        `;
    }


    /* ΧΙΟΝΟΝΕΡΟ */

    if([66,67].includes(code)){

        return `
            <span
                class="night-sleet"
                aria-label="Χιονόνερο">
            </span>
        `;
    }


    /* ΧΙΟΝΙ */

    if([71,73,75,77,85,86].includes(code)){

        if(isDay)
            return "🌨️";

        return `
            <span
                class="night-snow"
                aria-label="Νυχτερινό χιόνι">
            </span>
        `;
    }


    /* ΚΑΤΑΙΓΙΔΑ */

    if([95,96,99].includes(code)){

        if(isDay)
            return "⛈️";

        return `
            <span
                class="night-storm"
                aria-label="Νυχτερινή καταιγίδα">
            </span>
        `;
    }


    if(isDay)
        return "🌤️";

    return '<span class="night-moon">🌙</span>';
}


/* =====================================
   WEATHER TEXT
===================================== */

function weatherText(
    code,
    probability = 0,
    amount = 0
){

    const precipOK =
        Number(probability || 0) >= 30;


    if(!precipOK){

        if(code === 0)
            return "Αίθριος";

        if(code === 1)
            return "Κυρίως αίθριος";

        if(code === 2)
            return "Λίγες νεφώσεις";

        if(code === 3)
            return "Συννεφιά";

        if([45,48].includes(code))
            return "Ομίχλη";

        return "Μεταβλητός καιρός";
    }


    const intensity =
        precipitationIntensity(
            probability,
            amount
        );


    if([51,53,55,56,57].includes(code))
        return intensity + " ψιλόβροχο";


    if([61,63,65].includes(code))
        return intensity + " βροχή";


    if([80,81,82].includes(code))
        return intensity + " μπόρες";


    if([66,67].includes(code))
        return intensity + " χιονόνερο";


    if([71,73,75,77].includes(code))
        return intensity + " χιόνι";


    if([85,86].includes(code))
        return intensity + " χιονομπόρες";


    if([95,96,99].includes(code))
        return "Καταιγίδα";


    if(code === 0)
        return "Αίθριος";

    if(code === 1)
        return "Κυρίως αίθριος";

    if(code === 2)
        return "Λίγες νεφώσεις";

    if(code === 3)
        return "Συννεφιά";

    if([45,48].includes(code))
        return "Ομίχλη";


    return "Μεταβλητός καιρός";
}


/* =====================================
   WIND DIRECTION
===================================== */

function windDirection(degrees){

    if(
        degrees === null ||
        degrees === undefined ||
        isNaN(degrees)
    )
        return "—";


    const directions = [
        "Β","ΒΒΑ","ΒΑ","ΑΒΑ",
        "Α","ΑΝΑ","ΝΑ","ΝΝΑ",
        "Ν","ΝΝΔ","ΝΔ","ΔΝΔ",
        "Δ","ΔΒΔ","ΒΔ","ΒΒΔ"
    ];


    const index =
        Math.round(degrees / 22.5) % 16;


    return directions[index];
}


/* =====================================
   DATE
===================================== */

const greekDays = [
    "Κυρ",
    "Δευ",
    "Τρί",
    "Τετ",
    "Πέμ",
    "Παρ",
    "Σάβ"
];


function formatDate(dateString){

    const d =
        new Date(
            dateString + "T12:00:00"
        );


    return {

        day:
            greekDays[d.getDay()],

        date:
            d.getDate() +
            "/" +
            (d.getMonth()+1)
    };
}


/* =====================================
   ESCAPE HTML
===================================== */

function escapeHTML(value){

    return String(value ?? "")
        .replace(/&/g,"&amp;")
        .replace(/</g,"&lt;")
        .replace(/>/g,"&gt;")
        .replace(/"/g,"&quot;")
        .replace(/'/g,"&#039;");
}


/* =====================================
   SEARCH
===================================== */

async function searchCity(){

    const input =
        document.getElementById("cityInput");


    const city =
        input.value.trim();


    if(!city)
        return;


    lastCity = city;


    document.getElementById("forecast").innerHTML =
        `<div class="loading">
            Αναζήτηση πόλης...
         </div>`;


    try{

        const geoUrl =
            "https://geocoding-api.open-meteo.com/v1/search" +
            "?name=" +
            encodeURIComponent(city) +
            "&count=1" +
            "&language=el" +
            "&format=json";


        const response =
            await fetch(
                geoUrl,
                {cache:"no-store"}
            );


        if(!response.ok)
            throw new Error("Geocoding failed");


        const geo =
            await response.json();


        if(
            !geo.results ||
            !geo.results.length
        ){

            alert("Δεν βρέθηκε η πόλη.");

            return;
        }


        const place =
            geo.results[0];


        locationData = {

            name:place.name,

            latitude:place.latitude,

            longitude:place.longitude,

            country:place.country

        };


        await loadWeather();


    }catch(error){

        console.error(error);


        document.getElementById("forecast").innerHTML =
            `<div class="loading">
                Σφάλμα φόρτωσης δεδομένων.
             </div>`;
    }
}


/* =====================================
   LOAD WEATHER
===================================== */

async function loadWeather(){

    if(!locationData)
        return;


    const lat =
        locationData.latitude;

    const lon =
        locationData.longitude;


    const common =
        "latitude=" +
        encodeURIComponent(lat) +

        "&longitude=" +
        encodeURIComponent(lon) +

        "&timezone=auto" +

        "&forecast_days=15";


    const current =
        "temperature_2m," +
        "relative_humidity_2m," +
        "apparent_temperature," +
        "weather_code," +
        "wind_speed_10m," +
        "wind_direction_10m," +
        "is_day";


    const hourly =
        "temperature_2m," +
        "relative_humidity_2m," +
        "apparent_temperature," +
        "precipitation," +
        "precipitation_probability," +
        "weather_code," +
        "cloud_cover," +
        "wind_speed_10m," +
        "wind_direction_10m," +
        "wind_gusts_10m," +
        "is_day";


    const daily =
        "temperature_2m_max," +
        "temperature_2m_min," +
        "weather_code," +
        "precipitation_sum," +
        "precipitation_probability_max," +
        "wind_speed_10m_max," +
        "sunrise," +
        "sunset";


    const makeUrl =
        model =>

        "https://api.open-meteo.com/v1/forecast?" +
        common +
        "&current=" + current +
        "&hourly=" + hourly +
        "&daily=" + daily +
        "&models=" + model;


    const ecmwfUrl =
        makeUrl("ecmwf_ifs025");


    const gfsUrl =
        makeUrl("gfs_seamless");


    const iconUrl =
        makeUrl("icon_seamless");


    const [
        ecmwfRes,
        gfsRes,
        iconRes
    ] = await Promise.all([

        fetch(
            ecmwfUrl,
            {cache:"no-store"}
        ),

        fetch(
            gfsUrl,
            {cache:"no-store"}
        ),

        fetch(
            iconUrl,
            {cache:"no-store"}
        )

    ]);


    if(
        !ecmwfRes.ok ||
        !gfsRes.ok ||
        !iconRes.ok
    ){

        throw new Error(
            "Weather model request failed"
        );
    }


    const [
        ecmwf,
        gfs,
        icon
    ] = await Promise.all([

        ecmwfRes.json(),
        gfsRes.json(),
        iconRes.json()

    ]);


    weatherData = {
        ecmwf,
        gfs,
        icon
    };


    renderCurrent();

    renderForecast();


    /*
       Αν είχε ανοιχτεί ωριαία πρόγνωση,
       την ξανασχεδιάζουμε μετά το refresh.
    */

    if(
        selectedDayIndex !== null
    ){

        showHourly(
            selectedDayIndex,
            false
        );
    }
}


/* =====================================
   FIND CURRENT HOUR
===================================== */

function findCurrentHour(data){

    if(
        !data ||
        !data.hourly ||
        !data.hourly.time
    )
        return -1;


    const now =
        new Date();


    const localKey =
        now.getFullYear() +
        "-" +
        String(
            now.getMonth()+1
        ).padStart(2,"0") +
        "-" +
        String(
            now.getDate()
        ).padStart(2,"0") +
        "T" +
        String(
            now.getHours()
        ).padStart(2,"0");


    let best = -1;


    for(
        let i=0;
        i<data.hourly.time.length;
        i++
    ){

        if(
            data.hourly.time[i]
                .startsWith(localKey)
        ){

            best = i;
            break;
        }
    }


    return best;
}


/* =====================================
   CURRENT
===================================== */

function renderCurrent(){

    const d =
        weatherData.ecmwf;


    const temp =
        d.current.temperature_2m;


    const humidity =
        d.current.relative_humidity_2m;


    const wind =
        d.current.wind_speed_10m;


    const windDir =
        windDirection(
            d.current.wind_direction_10m
        );


    const feels =
        d.current.apparent_temperature;


    const code =
        d.current.weather_code;


    const isDay =
        d.current.is_day === 1;


    const currentIndex =
        findCurrentHour(d);


    let probability = 0;

    let precipitation = 0;


    if(currentIndex >= 0){

        probability =
            Number(
                d.hourly
                    .precipitation_probability[
                        currentIndex
                    ] || 0
            );


        precipitation =
            Number(
                d.hourly
                    .precipitation[
                        currentIndex
                    ] || 0
            );
    }


    const phenomenon =
        weatherText(
            code,
            probability,
            precipitation
        );


    document.getElementById("current").innerHTML = `

        <div class="current">

            <h2>
                ${escapeHTML(locationData.name)}
            </h2>

            <div class="temperature">
                ${Math.round(temp)}°C
            </div>

            <div class="condition">

                <span style="font-size:34px;
                             vertical-align:middle;
                             margin-right:8px;">

                    ${weatherIcon(
                        code,
                        isDay,
                        probability
                    )}

                </span>

                ${phenomenon}

            </div>


            <div class="current-grid">

                <div class="current-box">

                    <span>
                        💧 Υγρασία
                    </span>

                    <strong>
                        ${Math.round(humidity)}%
                    </strong>

                </div>


                <div class="current-box">

                    <span>
                        🌬️ Άνεμος
                    </span>

                    <strong>
                        ${Math.round(wind)}
                        km/h
                        —
                        ${windDir}
                    </strong>

                </div>


                <div class="current-box">

                    <span>
                        🌡️ Αίσθηση
                    </span>

                    <strong>
                        ${Math.round(feels)}°C
                    </strong>

                </div>

            </div>

        </div>

    `;
}


/* =====================================
   DAILY
===================================== */

function renderForecast(){

    const d =
        weatherData.ecmwf.daily;


    let html = "";


    for(
        let i=0;
        i<d.time.length;
        i++
    ){

        const date =
            formatDate(d.time[i]);


        const rain =
            Number(
                d.precipitation_probability_max[i] || 0
            );


        let precipitationInfo;


        if(rain >= 30){

            precipitationInfo =
                `💧 ${Math.round(rain)}%`;

        }else{

            precipitationInfo =
                `☁️ ${Math.round(rain)}%`;
        }


        html += `

            <div
                class="day"
                onclick="showHourly(${i})"
            >

                <div class="day-name">
                    ${date.day}
                </div>


                <div class="date">
                    ${date.date}
                </div>


                <div class="icon">

                    ${weatherIcon(
                        d.weather_code[i],
                        true,
                        rain
                    )}

                </div>


                <div class="temperatures">

                    <div class="max">
                        ${Math.round(
                            d.temperature_2m_max[i]
                        )}°
                    </div>

                    <div class="min">
                        ${Math.round(
                            d.temperature_2m_min[i]
                        )}°
                    </div>

                </div>


                <div class="rain">
                    ${precipitationInfo}
                </div>

            </div>

        `;
    }


    document.getElementById("forecast").innerHTML =
        html;
}


/* =====================================
   HOURLY
===================================== */

function showHourly(
    dayIndex,
    shouldScroll = true
){

    selectedDayIndex = dayIndex;


    const d =
        weatherData.ecmwf.hourly;


    const daily =
        weatherData.ecmwf.daily;


    const date =
        daily.time[dayIndex];


    const rows = [];


    for(
        let i=0;
        i<d.time.length;
        i++
    ){

        if(
            d.time[i].startsWith(date)
        ){

            rows.push(i);
        }
    }


    const formatted =
        formatDate(date);


    document.getElementById("hourlyTitle").innerText =
        "Πρόγνωση ανά ώρα — " +
        formatted.day +
        " " +
        formatted.date;


    let html = "";


    rows.forEach(i => {

        const hour =
            d.time[i].substring(11,16);


        const temp =
            Math.round(
                d.temperature_2m[i]
            );


        const feels =
            Math.round(
                d.apparent_temperature[i]
            );


        const rain =
            Number(
                d.precipitation_probability[i] || 0
            );


        const precipitation =
            Number(
                d.precipitation[i] || 0
            );


        const wind =
            Math.round(
                d.wind_speed_10m[i]
            );


        const windDir =
            windDirection(
                d.wind_direction_10m[i]
            );


        const clouds =
            Math.round(
                d.cloud_cover[i]
            );


        const isDay =
            d.is_day[i] === 1;


        const code =
            d.weather_code[i];


        const icon =
            weatherIcon(
                code,
                isDay,
                rain
            );


        /*
           ΦΑΙΝΟΜΕΝΟ

           >=30%:
           εμφανίζεται φαινόμενο.

           <30%:
           δεν εμφανίζεται υετός.
        */

        const phenomenon =
            weatherText(
                code,
                rain,
                precipitation
            );


        let precipitationHTML;


        if(rain >= 30){

            const intensity =
                precipitationIntensity(
                    rain,
                    precipitation
                );


            precipitationHTML = `

                <div class="precipitation">

                    💧

                    <b>
                        ${Math.round(rain)}%
                    </b>

                    <span>
                        • ${precipitation.toFixed(1)} mm
                    </span>

                </div>

                <div class="intensity">
                    ${intensity}
                </div>

            `;

        }else{

            /*
               Χωρίς κείμενο
               «Πιθανότητα υετού».
            */

            precipitationHTML = `

                <div class="precipitation-none">

                    💧 ${Math.round(rain)}%

                </div>

            `;
        }


        html += `

            <div class="hour">

                <div class="hour-time">
                    ${hour}
                </div>


                <div class="hour-icon">
                    ${icon}
                </div>


                <div class="hour-data">

                    🌡️
                    <b>${temp}°</b>

                    <br>

                    Αίσθηση ${feels}°

                </div>


                <div class="hour-data">

                    <b>
                        ${phenomenon}
                    </b>

                    <br>

                    ${precipitationHTML}

                </div>


                <div class="hour-data">

                    ☁️ ${clouds}%

                </div>


                <div class="hour-data">

                    🌬️
                    ${wind} km/h

                    <br>

                    <b>${windDir}</b>

                </div>

            </div>

        `;
    });


    document.getElementById("hourly").innerHTML =
        html;


    const section =
        document.getElementById(
            "hourlySection"
        );


    section.style.display = "block";


    if(shouldScroll){

        section.scrollIntoView({
            behavior:"smooth",
            block:"start"
        });
    }
}


/* =====================================
   CLOSE HOURLY
===================================== */

function closeHourly(){

    document.getElementById(
        "hourlySection"
    ).style.display = "none";


    selectedDayIndex = null;
}


/* =====================================
   ENTER
===================================== */

document
    .getElementById("cityInput")
    .addEventListener(
        "keydown",
        function(e){

            if(e.key === "Enter")
                searchCity();

        }
    );


/* =====================================
   INITIAL
===================================== */

searchCity();


/* =====================================
   SYNCHRONIZED 5-MINUTE REFRESH
===================================== */

/*
   Δεν χρησιμοποιούμε απλό setInterval(300000).

   Υπολογίζουμε το επόμενο ακριβές:

   xx:00
   xx:05
   xx:10
   xx:15
   xx:20
   ...

   και κάνουμε νέο network request.
*/

function scheduleFiveMinuteRefresh(){

    const now =
        new Date();


    const next =
        new Date(now);


    next.setSeconds(0,0);


    const currentMinutes =
        now.getMinutes();


    const nextBlock =
        Math.floor(
            currentMinutes / 5
        ) * 5 + 5;


    if(nextBlock >= 60){

        next.setHours(
            now.getHours() + 1
        );

        next.setMinutes(0);

    }else{

        next.setMinutes(
            nextBlock
        );
    }


    const delay =
        next.getTime() -
        now.getTime();


    setTimeout(
        async function(){

            if(locationData){

                try{

                    /*
                       cache:no-store
                       = νέο request.
                    */

                    await loadWeather();

                }catch(error){

                    console.error(
                        "Auto refresh error:",
                        error
                    );
                }
            }


            /*
               Μετά το request
               ξαναπρογραμματίζουμε
               το επόμενο ακριβές 5λεπτο.
            */

            scheduleFiveMinuteRefresh();

        },
        delay
    );
}


scheduleFiveMinuteRefresh();

</script>

</body>
</html>
