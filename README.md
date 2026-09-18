<!DOCTYPE html>
<html lang="el">

<head>

<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>


<style>

/* =====================================
   ΒΑΣΙΚΑ
===================================== */

*{
    box-sizing:border-box;
}

body{
    margin:0;

    font-family:
        Arial,
        Helvetica,
        sans-serif;

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

    background:
        rgba(3,20,38,.72);

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
   CURRENT WEATHER
===================================== */

.current{

    background:
        rgba(57,85,117,.72);

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

    grid-template-columns:
        repeat(3,1fr);

    gap:12px;
}

.current-box{

    background:
        rgba(104,133,165,.48);

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
   15 ΗΜΕΡΕΣ
===================================== */

.forecast{

    display:grid;

    grid-template-columns:
        repeat(6,1fr);

    gap:12px;
}

.day{

    background:
        rgba(53,84,119,.78);

    border-radius:17px;

    padding:18px 8px;

    text-align:center;

    cursor:pointer;

    transition:.18s;

    border:
        1px solid
        transparent;
}

.day:hover{

    transform:
        translateY(-3px);

    background:
        rgba(72,105,143,.95);

    border-color:
        rgba(255,255,255,.25);
}

.day:active{

    transform:
        scale(.97);
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

    height:40px;

    display:flex;

    align-items:center;

    justify-content:center;
}

.max{

    font-size:17px;

    font-weight:bold;
}

.min{

    margin-top:6px;

    color:#d0d7df;
}

.rain{

    margin-top:10px;

    font-size:12px;

    color:#c9e9ff;
}


/* =====================================
   ΝΥΧΤΕΡΙΝΑ ΕΙΚΟΝΙΔΙΑ
===================================== */

/*
   Το φεγγάρι είναι ένα μόνο emoji.
   Το κάνουμε ψυχρό/γκρι-μπλε.
*/

.night-moon{

    display:inline-block;

    filter:
        grayscale(1)
        brightness(.78)
        sepia(.10)
        hue-rotate(175deg);

    opacity:.90;
}


/*
   Νυχτερινή λίγη συννεφιά.

   ΔΕΝ χρησιμοποιούμε 🌙 + ☁️.

   Είναι ΕΝΑ ενιαίο οπτικό εικονίδιο,
   σχεδιασμένο με SVG, ώστε να φαίνεται
   σαν ένα weather emoji.
*/

.night-partly-cloudy{

    width:38px;

    height:38px;

    display:inline-block;

    vertical-align:middle;

    background:
        url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='25' cy='23' r='15' fill='%2395a9bd'/%3E%3Cpath d='M15 42c0-6.5 5.3-11.8 11.8-11.8 4.3 0 8.1 2.3 10.1 5.8 1.1-.4 2.3-.6 3.5-.6 6.3 0 11.4 5.1 11.4 11.4H15.8C15.3 45.6 15 43.8 15 42z' fill='%23c7d0d9'/%3E%3Cpath d='M20 38c1.5-4.6 5.8-7.9 10.9-7.9 4.1 0 7.7 2.1 9.8 5.3' fill='none' stroke='%23e2e7eb' stroke-width='2' stroke-linecap='round'/%3E%3C/svg%3E")

        center/

        contain

        no-repeat;
}


/* =====================================
   ΩΡΙΑΙΑ ΠΡΟΓΝΩΣΗ
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
   ΩΡΕΣ
===================================== */

.hourly{

    display:grid;

    gap:8px;
}

.hour{

    display:grid;

    grid-template-columns:
        70px
        50px
        1fr
        1fr
        1fr
        1fr;

    align-items:center;

    background:
        rgba(65,96,130,.62);

    border-radius:12px;

    padding:12px 10px;

    gap:8px;
}

.hour-time{

    font-weight:bold;
}

.hour-icon{

    font-size:25px;

    text-align:center;

    height:32px;

    display:flex;

    align-items:center;

    justify-content:center;
}

.hour-data{

    font-size:13px;

    color:#e4e8ed;

    line-height:1.5;
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
   TABLET / MOBILE
===================================== */

@media(max-width:750px){

    .forecast{

        grid-template-columns:
            repeat(3,1fr);
    }

    .current-grid{

        grid-template-columns:
            1fr;
    }

    .hour{

        grid-template-columns:
            55px
            40px
            1fr
            1fr;
    }

    .hour-data:nth-child(5),
    .hour-data:nth-child(6){

        display:none;
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

        grid-template-columns:
            repeat(3,1fr);

        gap:9px;
    }

    .day{

        padding:15px 5px;
    }

    .icon{

        font-size:30px;
    }

}

</style>

</head>


<body>


<div class="container">


    <!-- =================================
         HEADER
    ================================= -->

    <div class="header">

        <h1>
            🇬🇷 Greece Weather
        </h1>

        <p>
            Πρόγνωση καιρού για όλη την Ελλάδα
        </p>

    </div>


    <!-- =================================
         SEARCH
    ================================= -->

    <div class="search">

        <input
            id="cityInput"
            placeholder="Γράψε πόλη..."
            value="Θεσσαλονίκη"
        >

        <button
            onclick="searchCity()">

            Αναζήτηση

        </button>

    </div>


    <!-- =================================
         CURRENT
    ================================= -->

    <div id="current"></div>


    <!-- =================================
         15 DAYS
    ================================= -->

    <div class="section-title">

        📅 Πρόγνωση 15 ημερών

    </div>


    <div
        id="forecast"
        class="forecast">

        <div class="loading">

            Φόρτωση πρόγνωσης...

        </div>

    </div>


    <!-- =================================
         HOURLY
    ================================= -->

    <div
        id="hourlySection"
        class="hourly-section">


        <div class="hourly-header">

            <h3 id="hourlyTitle"></h3>


            <button
                class="close-hourly"
                onclick="closeHourly()">

                ✕ Κλείσιμο

            </button>

        </div>


        <div
            id="hourly"
            class="hourly">
        </div>


    </div>


    <!-- =================================
         INFO
    ================================= -->

    <div class="model-info">

        ECMWF IFS HRES • NOAA GFS • DWD ICON

        <br>

        Τα δεδομένα ανανεώνονται αυτόματα
        σύμφωνα με τους κύκλους έκδοσης
        των μοντέλων.

    </div>


</div>



<script>


/* =====================================
   GLOBAL
===================================== */

let weatherData = null;

let locationData = null;



/* =====================================
   WEATHER ICON
===================================== */

/*
   ΕΔΩ είναι η οριστική διόρθωση.

   code 0 = καθαρός
   code 1 = κυρίως αίθριος
   code 2 = λίγες νεφώσεις

   Τη νύχτα το code 2 ΔΕΝ επιστρέφει
   ΠΟΤΕ το 🌤️.

   Επιστρέφει το ενιαίο
   night-partly-cloudy icon.
*/

function weatherIcon(code, isDay = true){


    /* -----------------------------
       ΚΑΘΑΡΟΣ ΟΥΡΑΝΟΣ
    ----------------------------- */

    if(code === 0){

        if(isDay){

            return "☀️";

        }

        return '<span class="night-moon">🌙</span>';

    }



    /* -----------------------------
       ΚΥΡΙΩΣ ΑΙΘΡΙΟΣ
    ----------------------------- */

    if(code === 1){

        if(isDay){

            return "🌤️";

        }

        return '<span class="night-moon">🌙</span>';

    }



    /* -----------------------------
       ΛΙΓΕΣ ΝΕΦΩΣΕΙΣ
    ----------------------------- */

    if(code === 2){

        if(isDay){

            return "🌤️";

        }

        /*
           ΝΥΧΤΑ:

           ΕΝΑ ενιαίο εικονίδιο
           φεγγάρι + σύννεφο.

           ΠΟΤΕ 🌤️.
           ΠΟΤΕ δύο emoji.
        */

        return `
            <span
                class="night-partly-cloudy"
                aria-label="Λίγες νεφώσεις τη νύχτα">
            </span>
        `;

    }



    /* -----------------------------
       ΣΥΝΝΕΦΙΑ
    ----------------------------- */

    if(code === 3){

        return "☁️";

    }



    /* -----------------------------
       ΟΜΙΧΛΗ
    ----------------------------- */

    if(
        [45,48].includes(code)
    ){

        return "🌫️";

    }



    /* -----------------------------
       ΨΙΛΟΒΡΟΧΟ
    ----------------------------- */

    if(
        [51,53,55,56,57].includes(code)
    ){

        return "🌧️";

    }



    /* -----------------------------
       ΒΡΟΧΗ / ΧΙΟΝΟΝΕΡΟ
    ----------------------------- */

    if(
        [61,63,65,66,67].includes(code)
    ){

        return "🌧️";

    }



    /* -----------------------------
       ΧΙΟΝΙ
    ----------------------------- */

    if(
        [71,73,75,77].includes(code)
    ){

        return "🌨️";

    }



    /* -----------------------------
       ΜΠΟΡΕΣ
    ----------------------------- */

    if(
        [80,81,82].includes(code)
    ){

        return "🌦️";

    }



    /* -----------------------------
       ΧΙΟΝΟΜΠΟΡΕΣ
    ----------------------------- */

    if(
        [85,86].includes(code)
    ){

        return "🌨️";

    }



    /* -----------------------------
       ΚΑΤΑΙΓΙΔΑ
    ----------------------------- */

    if(
        [95,96,99].includes(code)
    ){

        return "⛈️";

    }



    /* -----------------------------
       FALLBACK
    ----------------------------- */

    if(isDay){

        return "🌤️";

    }

    return '<span class="night-moon">🌙</span>';

}



/* =====================================
   WEATHER TEXT
===================================== */

function weatherText(code){

    if(code === 0)
        return "Αίθριος";

    if(code === 1)
        return "Κυρίως αίθριος";

    if(code === 2)
        return "Λίγες νεφώσεις";

    if(code === 3)
        return "Συννεφιά";

    if(
        [45,48].includes(code)
    )
        return "Ομίχλη";

    if(
        [51,53,55,56,57].includes(code)
    )
        return "Ψιλόβροχο";

    if(
        [61,63,65].includes(code)
    )
        return "Βροχή";

    if(
        [66,67].includes(code)
    )
        return "Χιονόνερο";

    if(
        [71,73,75,77].includes(code)
    )
        return "Χιόνι";

    if(
        [80,81,82].includes(code)
    )
        return "Μπόρες";

    if(
        [85,86].includes(code)
    )
        return "Χιονομπόρες";

    if(
        [95,96,99].includes(code)
    )
        return "Καταιγίδα";

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
    ){

        return "—";

    }


    const directions = [

        "Β",
        "ΒΒΑ",
        "ΒΑ",
        "ΑΒΑ",
        "Α",
        "ΑΝΑ",
        "ΝΑ",
        "ΝΝΑ",
        "Ν",
        "ΝΝΔ",
        "ΝΔ",
        "ΔΝΔ",
        "Δ",
        "ΔΒΔ",
        "ΒΔ",
        "ΒΒΔ"

    ];


    const index =
        Math.round(
            degrees / 22.5
        ) % 16;


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
            dateString +
            "T12:00:00"
        );


    return {

        day:
            greekDays[d.getDay()],

        date:
            d.getDate() +
            "/" +
            (d.getMonth() + 1)

    };

}



/* =====================================
   SEARCH CITY
===================================== */

async function searchCity(){


    const city =
        document
        .getElementById("cityInput")
        .value
        .trim();


    if(!city)
        return;


    document
        .getElementById("forecast")
        .innerHTML =

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
            await fetch(geoUrl);


        const geo =
            await response.json();


        if(
            !geo.results ||
            !geo.results.length
        ){

            alert(
                "Δεν βρέθηκε η πόλη."
            );

            return;

        }


        const place =
            geo.results[0];


        locationData = {

            name:
                place.name,

            latitude:
                place.latitude,

            longitude:
                place.longitude,

            country:
                place.country

        };


        await loadWeather();


    }catch(error){


        console.error(error);


        document
            .getElementById("forecast")
            .innerHTML =

            `<div class="loading">

                Σφάλμα φόρτωσης δεδομένων.

             </div>`;

    }

}



/* =====================================
   LOAD WEATHER
===================================== */

async function loadWeather(){


    const lat =
        locationData.latitude;


    const lon =
        locationData.longitude;



    const common =

        "latitude=" +
        lat +

        "&longitude=" +
        lon +

        "&timezone=auto" +

        "&forecast_days=15";



    /* CURRENT */

    const current =

        "temperature_2m," +

        "relative_humidity_2m," +

        "apparent_temperature," +

        "weather_code," +

        "wind_speed_10m," +

        "wind_direction_10m," +

        "is_day";



    /* HOURLY */

    const hourly =

        "temperature_2m," +

        "relative_humidity_2m," +

        "apparent_temperature," +

        "precipitation," +

        "precipitation_probability," +

        "snowfall," +

        "weather_code," +

        "cloud_cover," +

        "wind_speed_10m," +

        "wind_direction_10m," +

        "wind_gusts_10m," +

        "is_day";



    /* DAILY */

    const daily =

        "temperature_2m_max," +

        "temperature_2m_min," +

        "weather_code," +

        "precipitation_sum," +

        "precipitation_probability_max," +

        "snowfall_sum," +

        "wind_speed_10m_max," +

        "sunrise," +

        "sunset";



    /* ECMWF */

    const ecmwfUrl =

        "https://api.open-meteo.com/v1/forecast?" +

        common +

        "&current=" +
        current +

        "&hourly=" +
        hourly +

        "&daily=" +
        daily +

        "&models=ecmwf_ifs025";



    /* GFS */

    const gfsUrl =

        "https://api.open-meteo.com/v1/forecast?" +

        common +

        "&current=" +
        current +

        "&hourly=" +
        hourly +

        "&daily=" +
        daily +

        "&models=gfs_seamless";



    /* ICON */

    const iconUrl =

        "https://api.open-meteo.com/v1/forecast?" +

        common +

        "&current=" +
        current +

        "&hourly=" +
        hourly +

        "&daily=" +
        daily +

        "&models=icon_seamless";



    const [

        ecmwfRes,
        gfsRes,
        iconRes

    ] = await Promise.all([

        fetch(ecmwfUrl),

        fetch(gfsUrl),

        fetch(iconUrl)

    ]);



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

        ecmwf:
            ecmwf,

        gfs:
            gfs,

        icon:
            icon

    };



    renderCurrent();

    renderForecast();

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



    document
        .getElementById("current")
        .innerHTML = `

        <div class="current">

            <h2>
                ${locationData.name}
            </h2>

            <div class="temperature">

                ${Math.round(temp)}°C

            </div>

            <div class="condition">

                ${weatherIcon(
                    code,
                    isDay
                )}

                ${weatherText(code)}

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
   DAILY FORECAST
===================================== */

function renderForecast(){


    const d =
        weatherData.ecmwf.daily;


    let html = "";


    for(
        let i = 0;
        i < d.time.length;
        i++
    ){


        const date =
            formatDate(
                d.time[i]
            );


        const rain =
            d.precipitation_probability_max[i]
            || 0;


        const snow =
            Number(
                d.snowfall_sum[i]
                || 0
            );



        let precipitationInfo = "";


        if(snow > 0){

            precipitationInfo =

                `❄️ ${snow.toFixed(1)} cm`;

        }else{

            precipitationInfo =

                `💧 ${Math.round(rain)}%`;

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
                    true
                )}

            </div>


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


            <div class="rain">

                ${precipitationInfo}

            </div>


        </div>

        `;

    }


    document
        .getElementById("forecast")
        .innerHTML =
        html;

}



/* =====================================
   HOURLY
===================================== */

function showHourly(dayIndex){


    const d =
        weatherData.ecmwf.hourly;


    const date =
        weatherData
        .ecmwf
        .daily
        .time[dayIndex];


    const rows = [];


    for(
        let i = 0;
        i < d.time.length;
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


    document
        .getElementById("hourlyTitle")
        .innerText =

        "Πρόγνωση ανά ώρα — " +

        formatted.day +

        " " +

        formatted.date;


    let html = "";


    rows.forEach(i => {


        const hour =
            d.time[i]
            .substring(11,16);


        const temp =
            Math.round(
                d.temperature_2m[i]
            );


        const feels =
            Math.round(
                d.apparent_temperature[i]
            );


        const rain =
            Math.round(
                d.precipitation_probability[i]
                || 0
            );


        const precipitation =
            Number(
                d.precipitation[i]
                || 0
            ).toFixed(1);


        const snowfall =
            Number(
                d.snowfall[i]
                || 0
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


        /*
           ΕΔΩ καλείται η διορθωμένη
           weatherIcon().

           Άρα:

           ημέρα + λίγες νεφώσεις
           → 🌤️

           νύχτα + λίγες νεφώσεις
           → ΕΝΑ ενιαίο εικονίδιο
             φεγγάρι/σύννεφο

           ΠΟΤΕ 🌤️ τη νύχτα.
        */

        const icon =
            weatherIcon(
                d.weather_code[i],
                isDay
            );


        let precipitationHTML = "";


        if(snowfall > 0){

            precipitationHTML = `

                ❄️ Χιόνι:
                <b>
                    ${snowfall.toFixed(1)} cm
                </b>

                <br>

                💧 ${rain}%

            `;

        }else{

            precipitationHTML = `

                💧 ${rain}%

                <br>

                ${precipitation} mm

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

                <b>
                    ${temp}°
                </b>

                <br>

                Αίσθηση
                ${feels}°

            </div>


            <div class="hour-data">

                ${precipitationHTML}

            </div>


            <div class="hour-data">

                ☁️
                ${clouds}%

            </div>


            <div class="hour-data">

                🌬️
                ${wind} km/h

                <br>

                Διεύθυνση:
                <b>
                    ${windDir}
                </b>

            </div>


        </div>

        `;

    });


    document
        .getElementById("hourly")
        .innerHTML =
        html;


    const section =
        document
        .getElementById(
            "hourlySection"
        );


    section.style.display =
        "block";


    section.scrollIntoView({

        behavior:"smooth",

        block:"start"

    });

}



/* =====================================
   CLOSE HOURLY
===================================== */

function closeHourly(){

    document
        .getElementById(
            "hourlySection"
        )
        .style.display =
        "none";

}



/* =====================================
   ENTER SEARCH
===================================== */

document
    .getElementById("cityInput")
    .addEventListener(
        "keydown",
        function(e){

            if(e.key === "Enter"){

                searchCity();

            }

        }
    );



/* =====================================
   INITIAL LOAD
===================================== */

searchCity();


</script>


</body>

</html>
