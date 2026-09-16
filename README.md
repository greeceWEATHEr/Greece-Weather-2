<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>WORLD WEATHER</title>

<link rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

<style>
*{
  box-sizing:border-box;
}

html,body{
  margin:0;
  padding:0;
  min-height:100%;
  font-family:Arial,sans-serif;
  background:#07152d;
  color:#fff;
}

body{
  overflow-x:hidden;
}

.container{
  width:min(1100px,94%);
  margin:auto;
  padding:20px 0 40px;
}

header{
  text-align:center;
  padding:15px 0 20px;
}

.logo{
  font-size:30px;
  font-weight:800;
  letter-spacing:1px;
}

.subtitle{
  margin-top:6px;
  color:#a9c3e8;
  font-size:14px;
}

.search-area{
  display:flex;
  gap:10px;
  margin:15px 0;
}

#searchInput{
  flex:1;
  min-width:0;
  padding:15px;
  border:none;
  outline:none;
  border-radius:14px;
  background:#10294b;
  color:white;
  font-size:16px;
}

#searchInput::placeholder{
  color:#91a7c6;
}

button{
  border:0;
  border-radius:13px;
  padding:13px 17px;
  cursor:pointer;
  background:#1c65d1;
  color:white;
  font-weight:700;
}

button:disabled{
  opacity:.5;
  cursor:not-allowed;
}

.results{
  display:grid;
  gap:8px;
  margin-bottom:15px;
}

.result{
  width:100%;
  text-align:left;
  background:#10294b;
  border:1px solid #244873;
}

.quick{
  display:flex;
  gap:8px;
  flex-wrap:wrap;
  margin-bottom:18px;
}

.quick button{
  background:#10294b;
  font-size:13px;
}

.card{
  background:#0d2341;
  border:1px solid #1b416b;
  border-radius:20px;
  padding:20px;
  margin-bottom:18px;
}

.location-title{
  font-size:26px;
  font-weight:800;
}

.location-sub{
  margin-top:5px;
  color:#9db8db;
}

.live-label{
  display:inline-block;
  margin-top:14px;
  padding:6px 10px;
  border-radius:20px;
  background:#173d2d;
  color:#8ee0ad;
  font-size:12px;
  font-weight:bold;
}

.live-grid{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
  margin-top:16px;
}

.live-item{
  background:#102b4d;
  border-radius:15px;
  padding:15px;
}

.live-value{
  font-size:23px;
  font-weight:800;
}

.live-name{
  color:#91acd0;
  font-size:12px;
  margin-top:5px;
}

.status{
  margin-top:12px;
  color:#9eb5d4;
  font-size:13px;
}

.section-title{
  font-size:22px;
  margin:8px 0 14px;
}

.model-info{
  color:#91acd0;
  font-size:13px;
  margin-bottom:15px;
}

.forecast{
  display:grid;
  grid-template-columns:repeat(5,1fr);
  gap:10px;
}

.day{
  background:#102b4d;
  border-radius:16px;
  padding:13px;
  text-align:center;
  min-height:190px;
}

.day-name{
  font-weight:700;
  margin-bottom:8px;
}

.icon{
  font-size:30px;
  margin:5px 0;
}

.temps{
  display:flex;
  flex-direction:column;
  align-items:center;
  gap:2px;
  font-size:19px;
  font-weight:800;
}

.high{
  color:white;
}

.low{
  color:#9ebbe0;
}

.rain{
  margin-top:8px;
  color:#80baff;
  font-size:12px;
}

.map-title{
  font-size:20px;
  margin-bottom:12px;
}

#map{
  height:380px;
  width:100%;
  border-radius:17px;
  overflow:hidden;
}

.error{
  background:#4a1c25;
  border:1px solid #8d3947;
  color:#ffd5da;
  padding:13px;
  border-radius:12px;
  margin-bottom:15px;
}

.loading{
  opacity:.72;
  pointer-events:none;
}

@media(max-width:800px){

  .forecast{
    grid-template-columns:repeat(3,1fr);
  }

  .live-grid{
    grid-template-columns:repeat(2,1fr);
  }
}

@media(max-width:500px){

  .search-area{
    flex-direction:column;
  }

  .forecast{
    grid-template-columns:repeat(2,1fr);
  }

  .logo{
    font-size:25px;
  }

  #map{
    height:300px;
  }
}
</style>
</head>

<body>

<div class="container">

<header>

  <div class="logo">
    🌍 WORLD WEATHER
  </div>

  <div class="subtitle">
    Global weather forecast
  </div>

</header>


<!-- SEARCH -->

<div class="search-area">

  <input
    id="searchInput"
    type="text"
    placeholder="Αναζήτησε πόλη ή περιοχή οπουδήποτε στον κόσμο..."
    autocomplete="off"
  >

  <button id="searchBtn">
    Αναζήτηση
  </button>

</div>


<div id="results" class="results"></div>


<!-- QUICK CITIES -->

<div class="quick">

  <button data-city="Thessaloniki">
    Θεσσαλονίκη
  </button>

  <button data-city="Athens">
    Αθήνα
  </button>

  <button data-city="London">
    Λονδίνο
  </button>

  <button data-city="New York">
    New York
  </button>

  <button data-city="Tokyo">
    Tokyo
  </button>

  <button data-city="Seoul">
    Seoul
  </button>

</div>


<div id="errorBox"></div>


<!-- CURRENT -->

<div class="card">

  <div id="locationTitle"
       class="location-title">
    Θεσσαλονίκη
  </div>

  <div id="locationSub"
       class="location-sub">
    Ελλάδα
  </div>


  <div class="live-label">
    ● LIVE
  </div>


  <div class="live-grid">

    <div class="live-item">

      <div id="liveTemp"
           class="live-value">
        —
      </div>

      <div class="live-name">
        Θερμοκρασία
      </div>

    </div>


    <div class="live-item">

      <div id="liveHumidity"
           class="live-value">
        —
      </div>

      <div class="live-name">
        Υγρασία
      </div>

    </div>


    <div class="live-item">

      <div id="liveWind"
           class="live-value">
        —
      </div>

      <div class="live-name">
        Άνεμος
      </div>

    </div>


    <div class="live-item">

      <div id="liveDirection"
           class="live-value">
        —
      </div>

      <div class="live-name">
        Διεύθυνση
      </div>

    </div>

  </div>


  <div id="liveStatus"
       class="status">
    Φόρτωση τρεχουσών συνθηκών...
  </div>

</div>


<!-- FORECAST -->

<div class="card">

  <div class="section-title">
    📅 15ήμερη πρόγνωση
  </div>


  <div class="model-info">
    Μέσος όρος ECMWF IFS HRES 9 km + ECMWF AIFS 0.25°
  </div>


  <div id="forecast"
       class="forecast">

  </div>

</div>


<!-- MAP -->

<div class="card">

  <div class="map-title">
    📍 Τοποθεσία
  </div>

  <div id="map"></div>

</div>

</div>


<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>


<script>

/* =========================================================
   API
   ========================================================= */

const GEOCODING_API =
  "https://geocoding-api.open-meteo.com/v1/search";

const IFS_API =
  "https://api.open-meteo.com/v1/ecmwf";

const FORECAST_API =
  "https://api.open-meteo.com/v1/forecast";


/* =========================================================
   STATE
   ========================================================= */

let activeController = null;

let requestId = 0;

let map = null;

let marker = null;


/* =========================================================
   DOM
   ========================================================= */

const searchInput =
  document.getElementById("searchInput");

const searchBtn =
  document.getElementById("searchBtn");

const results =
  document.getElementById("results");

const errorBox =
  document.getElementById("errorBox");

const forecast =
  document.getElementById("forecast");

const locationTitle =
  document.getElementById("locationTitle");

const locationSub =
  document.getElementById("locationSub");

const liveTemp =
  document.getElementById("liveTemp");

const liveHumidity =
  document.getElementById("liveHumidity");

const liveWind =
  document.getElementById("liveWind");

const liveDirection =
  document.getElementById("liveDirection");

const liveStatus =
  document.getElementById("liveStatus");


/* =========================================================
   FETCH WITH TIMEOUT
   ========================================================= */

async function getJSON(
  url,
  controller,
  timeout = 15000
){

  const timer =
    setTimeout(
      () => controller.abort(),
      timeout
    );

  try{

    const response =
      await fetch(
        url,
        {
          signal:controller.signal,
          cache:"no-store"
        }
      );

    if(!response.ok){

      throw new Error(
        "HTTP " + response.status
      );

    }

    return await response.json();

  }finally{

    clearTimeout(timer);

  }

}


/* =========================================================
   AVERAGE
   ========================================================= */

function average(a,b){

  if(
    typeof a !== "number" ||
    typeof b !== "number"
  ){

    return null;

  }

  return (a+b)/2;

}


/* =========================================================
   WIND DIRECTION AVERAGE
   ========================================================= */

function averageDirection(a,b){

  if(
    typeof a !== "number" ||
    typeof b !== "number"
  ){

    return null;

  }

  const r1 =
    a * Math.PI / 180;

  const r2 =
    b * Math.PI / 180;


  const x =
    Math.cos(r1) +
    Math.cos(r2);

  const y =
    Math.sin(r1) +
    Math.sin(r2);


  let result =
    Math.atan2(y,x)
    * 180 / Math.PI;


  if(result < 0){

    result += 360;

  }


  return result;

}


/* =========================================================
   DIRECTION TEXT
   ========================================================= */

function directionText(degrees){

  if(
    typeof degrees !== "number"
  ){

    return "—";

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
    Math.round(degrees / 45) % 8;


  return directions[index];

}


/* =========================================================
   WEATHER ICON
   ========================================================= */

function weatherIcon(code){

  if(code === 0)
    return "☀️";

  if(code === 1)
    return "🌤️";

  if(code === 2)
    return "⛅";

  if(code === 3)
    return "☁️";

  if(
    code === 45 ||
    code === 48
  )
    return "🌫️";

  if(
    [51,53,55,56,57].includes(code)
  )
    return "🌦️";

  if(
    [61,63,65,66,67].includes(code)
  )
    return "🌧️";

  if(
    [71,73,75,77].includes(code)
  )
    return "❄️";

  if(
    [80,81,82].includes(code)
  )
    return "🌦️";

  if(
    [85,86].includes(code)
  )
    return "🌨️";

  if(
    [95,96,99].includes(code)
  )
    return "⛈️";

  return "🌤️";

}


/* =========================================================
   IFS HRES 9 KM
   ========================================================= */

function createIFSUrl(
  latitude,
  longitude
){

  const params =
    new URLSearchParams({

      latitude,
      longitude,

      timezone:"auto",

      forecast_days:"15",

      hourly:
        [
          "temperature_2m",
          "relative_humidity_2m",
          "wind_speed_10m",
          "wind_direction_10m",
          "weather_code",
          "precipitation",
          "rain",
          "snowfall"
        ].join(","),

      daily:
        [
          "temperature_2m_max",
          "temperature_2m_min",
          "precipitation_sum",
          "rain_sum",
          "snowfall_sum",
          "weather_code"
        ].join(",")

    });


  return (
    IFS_API +
    "?" +
    params.toString()
  );

}


/* =========================================================
   AIFS 0.25 KM
   ========================================================= */

function createAIFSUrl(
  latitude,
  longitude
){

  const params =
    new URLSearchParams({

      latitude,
      longitude,

      timezone:"auto",

      forecast_days:"15",

      models:"ecmwf_aifs025",

      hourly:
        [
          "temperature_2m",
          "relative_humidity_2m",
          "wind_speed_10m",
          "wind_direction_10m",
          "weather_code",
          "precipitation",
          "rain",
          "snowfall"
        ].join(","),

      daily:
        [
          "temperature_2m_max",
          "temperature_2m_min",
          "precipitation_sum",
          "rain_sum",
          "snowfall_sum",
          "weather_code"
        ].join(",")

    });


  return (
    FORECAST_API +
    "?" +
    params.toString()
  );

}


/* =========================================================
   GET BOTH MODELS
   ========================================================= */

async function getModels(
  latitude,
  longitude,
  controller
){

  const ifsPromise =
    getJSON(
      createIFSUrl(
        latitude,
        longitude
      ),
      controller
    );


  const aifsPromise =
    getJSON(
      createAIFSUrl(
        latitude,
        longitude
      ),
      controller
    );


  return Promise.all([
    ifsPromise,
    aifsPromise
  ]);

}


/* =========================================================
   FIND CURRENT HOUR
   ========================================================= */

function getCurrentIndex(
  times
){

  if(
    !Array.isArray(times) ||
    times.length === 0
  ){

    return 0;

  }


  const now =
    Date.now();


  let closestIndex = 0;

  let closestDifference =
    Infinity;


  for(
    let i=0;
    i<times.length;
    i++
  ){

    const time =
      new Date(
        times[i]
      ).getTime();


    const difference =
      Math.abs(
        time - now
      );


    if(
      difference <
      closestDifference
    ){

      closestDifference =
        difference;

      closestIndex =
        i;

    }

  }


  return closestIndex;

}


/* =========================================================
   CURRENT CONDITIONS
   ========================================================= */

function renderCurrent(
  ifs,
  aifs
){

  const i1 =
    getCurrentIndex(
      ifs.hourly.time
    );

  const i2 =
    getCurrentIndex(
      aifs.hourly.time
    );


  const temperature =
    average(
      ifs.hourly.temperature_2m[i1],
      aifs.hourly.temperature_2m[i2]
    );


  const humidity =
    average(
      ifs.hourly.relative_humidity_2m[i1],
      aifs.hourly.relative_humidity_2m[i2]
    );


  const wind =
    average(
      ifs.hourly.wind_speed_10m[i1],
      aifs.hourly.wind_speed_10m[i2]
    );


  const direction =
    averageDirection(
      ifs.hourly.wind_direction_10m[i1],
      aifs.hourly.wind_direction_10m[i2]
    );


  liveTemp.textContent =
    temperature !== null
      ? Math.round(temperature) + "°"
      : "—";


  liveHumidity.textContent =
    humidity !== null
      ? Math.round(humidity) + "%"
      : "—";


  liveWind.textContent =
    wind !== null
      ? Math.round(wind) + " km/h"
      : "—";


  liveDirection.textContent =
    direction !== null
      ? directionText(direction)
      : "—";


  liveStatus.textContent =
    "Τρέχουσες τιμές των δύο ECMWF μοντέλων.";

}


/* =========================================================
   15 DAY FORECAST
   ========================================================= */

function renderForecast(
  ifs,
  aifs
){

  const d1 =
    ifs.daily;

  const d2 =
    aifs.daily;


  if(
    !d1 ||
    !d2 ||
    !d1.time ||
    !d2.time
  ){

    throw new Error(
      "Missing daily forecast"
    );

  }


  const count =
    Math.min(
      15,
      d1.time.length,
      d2.time.length
    );


  forecast.innerHTML = "";


  for(
    let i=0;
    i<count;
    i++
  ){

    const high =
      average(
        d1.temperature_2m_max[i],
        d2.temperature_2m_max[i]
      );


    const low =
      average(
        d1.temperature_2m_min[i],
        d2.temperature_2m_min[i]
      );


    const precipitation =
      average(
        d1.precipitation_sum[i],
        d2.precipitation_sum[i]
      );


    const rain =
      average(
        d1.rain_sum[i],
        d2.rain_sum[i]
      );


    const snow =
      average(
        d1.snowfall_sum[i],
        d2.snowfall_sum[i]
      );


    /*
      ΔΕΝ παίρνουμε μέσο όρο των αριθμών WMO.
      Η βροχή/το χιόνι υπολογίζονται από τα
      πραγματικά precipitation fields.
    */

    let code =
      Number(
        d1.weather_code[i]
      );


    if(
      snow !== null &&
      snow > 0.1 &&
      snow >= (rain || 0)
    ){

      code = 71;

    }
    else if(
      rain !== null &&
      rain > 0.1
    ){

      code = 61;

    }


    const date =
      new Date(
        d1.time[i] +
        "T12:00:00"
      );


    const dayName =
      date.toLocaleDateString(
        "el-GR",
        {
          weekday:"short"
        }
      );


    const dateText =
      date.toLocaleDateString(
        "el-GR",
        {
          day:"numeric",
          month:"numeric"
        }
      );


    const card =
      document.createElement(
        "div"
      );


    card.className =
      "day";


    card.innerHTML = `

      <div class="day-name">
        ${dayName}<br>
        ${dateText}
      </div>

      <div class="icon">
        ${weatherIcon(code)}
      </div>

      <div class="temps">

        <div class="high">
          ${
            high !== null
              ? Math.round(high) + "°"
              : "—"
          }
        </div>

        <div class="low">
          ${
            low !== null
              ? Math.round(low) + "°"
              : "—"
          }
        </div>

      </div>

      <div class="rain">
        💧 ${
          precipitation !== null
            ? precipitation.toFixed(1)
              + " mm"
            : "—"
        }
      </div>

    `;


    forecast.appendChild(
      card
    );

  }

}


/* =========================================================
   MAP
   ========================================================= */

function initMap(){

  if(map)
    return;


  map =
    L.map(
      "map",
      {
        zoomControl:true
      }
    ).setView(
      [40.64,22.94],
      6
    );


  L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
      maxZoom:19,
      attribution:
        "&copy; OpenStreetMap contributors"
    }
  ).addTo(map);

}


function updateMap(
  latitude,
  longitude,
  name
){

  initMap();


  map.setView(
    [
      latitude,
      longitude
    ],
    9,
    {
      animate:false
    }
  );


  if(marker){

    map.removeLayer(
      marker
    );

  }


  marker =
    L.marker(
      [
        latitude,
        longitude
      ]
    )
    .addTo(map)
    .bindPopup(
      name
    )
    .openPopup();


  setTimeout(
    () => map.invalidateSize(),
    150
  );

}


/* =========================================================
   LOCATION
   ========================================================= */

async function loadLocation(
  place
){

  /*
    Σταματάμε οποιοδήποτε προηγούμενο request.
    Έτσι δεν μπορούν δύο αναζητήσεις να
    γράψουν ταυτόχρονα στη σελίδα.
  */

  if(activeController){

    activeController.abort();

  }


  activeController =
    new AbortController();


  const controller =
    activeController;


  const thisRequest =
    ++requestId;


  document.body.classList.add(
    "loading"
  );


  locationTitle.textContent =
    place.name;


  locationSub.textContent =
    place.country || "";


  liveTemp.textContent =
    "—";

  liveHumidity.textContent =
    "—";

  liveWind.textContent =
    "—";

  liveDirection.textContent =
    "—";


  liveStatus.textContent =
    "Φόρτωση τρεχουσών συνθηκών...";


  forecast.innerHTML =
    `
      <div class="status">
        Φόρτωση 15ήμερης πρόγνωσης...
      </div>
    `;


  errorBox.innerHTML =
    "";


  try{

    const [
      ifs,
      aifs
    ] =
      await getModels(
        place.latitude,
        place.longitude,
        controller
      );


    /*
      Αν ο χρήστης έχει ήδη ζητήσει
      άλλη περιοχή, πετάμε το παλιό αποτέλεσμα.
    */

    if(
      thisRequest !== requestId
    ){

      return;

    }


    renderCurrent(
      ifs,
      aifs
    );


    renderForecast(
      ifs,
      aifs
    );


    updateMap(
      place.latitude,
      place.longitude,
      place.name
    );


  }
  catch(error){

    if(
      error.name ===
      "AbortError"
    ){

      return;

    }


    console.error(
      error
    );


    forecast.innerHTML =
      "";


    errorBox.innerHTML =
      `
        <div class="error">
          Δεν ήταν δυνατή η φόρτωση
          των δεδομένων αυτή τη στιγμή.
          Δοκίμασε ξανά.
        </div>
      `;


    liveStatus.textContent =
      "Τα δεδομένα δεν ήταν διαθέσιμα.";

  }
  finally{

    if(
      thisRequest === requestId
    ){

      document.body.classList.remove(
        "loading"
      );

    }

  }

}


/* =========================================================
   SEARCH
   ========================================================= */

async function searchPlaces(
  text
){

  text =
    text.trim();


  if(!text)
    return;


  results.innerHTML =
    `
      <div class="status">
        Αναζήτηση...
      </div>
    `;


  const controller =
    new AbortController();


  try{

    const params =
      new URLSearchParams({

        name:text,

        count:"20",

        language:"el",

        format:"json"

      });


    const data =
      await getJSON(
        GEOCODING_API +
        "?" +
        params.toString(),
        controller
      );


    results.innerHTML =
      "";


    if(
      !data.results ||
      data.results.length === 0
    ){

      results.innerHTML =
        `
          <div class="status">
            Δεν βρέθηκε περιοχή.
          </div>
        `;

      return;

    }


    data.results.forEach(
      place => {

        const button =
          document.createElement(
            "button"
          );


        button.className =
          "result";


        button.textContent =
          `${place.name}${
            place.admin1
              ? " · " + place.admin1
              : ""
          } · ${
            place.country || ""
          }`;


        button.onclick =
          () => {

            results.innerHTML =
              "";


            loadLocation({

              name:
                place.name,

              country:
                place.country,

              latitude:
                Number(
                  place.latitude
                ),

              longitude:
                Number(
                  place.longitude
                )

            });

          };


        results.appendChild(
          button
        );

      }
    );

  }
  catch(error){

    if(
      error.name !==
      "AbortError"
    ){

      results.innerHTML =
        `
          <div class="status">
            Η αναζήτηση απέτυχε.
          </div>
        `;

    }

  }

}


/* =========================================================
   EVENTS
   ========================================================= */

searchBtn.onclick =
  () =>
    searchPlaces(
      searchInput.value
    );


searchInput.addEventListener(
  "keydown",
  event => {

    if(
      event.key === "Enter"
    ){

      event.preventDefault();

      searchPlaces(
        searchInput.value
      );

    }

  }
);


document
  .querySelectorAll(
    ".quick button"
  )
  .forEach(
    button => {

      button.onclick =
        () => {

          searchInput.value =
            button.dataset.city;


          searchPlaces(
            button.dataset.city
          );

        };

    }
  );


/* =========================================================
   START
   ========================================================= */

loadLocation({

  name:
    "Θεσσαλονίκη",

  country:
    "Ελλάδα",

  latitude:
    40.6401,

  longitude:
    22.9444

});

</script>

</body>
</html>
