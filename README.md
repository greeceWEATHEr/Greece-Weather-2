<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<link rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

<style>

*{
  box-sizing:border-box;
}

body{
  margin:0;
  font-family:Arial,sans-serif;
  background:linear-gradient(180deg,#071a2d,#0d304b);
  color:white;
}

header{
  text-align:center;
  padding:28px 15px;
  background:rgba(0,0,0,.25);
}

header h1{
  margin:0;
  font-size:30px;
}

header p{
  margin:8px 0 0;
  opacity:.8;
}

.container{
  max-width:1100px;
  margin:auto;
  padding:20px;
}

.search{
  display:flex;
  gap:10px;
  margin-bottom:25px;
}

.search input{
  flex:1;
  min-width:0;
  padding:14px;
  border:none;
  border-radius:12px;
  font-size:16px;
  outline:none;
}

.search button{
  border:none;
  border-radius:12px;
  padding:0 20px;
  background:#2196f3;
  color:white;
  font-size:16px;
  cursor:pointer;
}

.section-title{
  font-size:20px;
  font-weight:bold;
  margin:25px 0 12px;
}

.city-buttons{
  display:flex;
  flex-wrap:wrap;
  gap:8px;
}

.city-buttons button{
  border:none;
  border-radius:10px;
  padding:10px 14px;
  background:#173d5c;
  color:white;
  cursor:pointer;
  font-size:14px;
}

.city-buttons button:hover{
  background:#245b84;
}

.current{
  margin-top:25px;
  padding:22px;
  border-radius:18px;
  background:rgba(255,255,255,.09);
}

.city-name{
  font-size:28px;
  font-weight:bold;
}

.temp{
  font-size:52px;
  font-weight:bold;
  margin:10px 0;
}

.status{
  font-size:18px;
  opacity:.9;
}

.forecast{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(135px,1fr));
  gap:10px;
  margin-top:15px;
}

.day{
  padding:15px;
  border-radius:15px;
  background:rgba(255,255,255,.09);
  text-align:center;
}

.day-date{
  font-weight:bold;
  margin-bottom:8px;
}

.weather-icon{
  font-size:38px;
  margin:6px 0;
}

.weather-text{
  min-height:35px;
  font-size:14px;
  opacity:.9;
}

.max{
  font-size:23px;
  font-weight:bold;
  margin-top:8px;
}

.min{
  margin-top:5px;
  opacity:.7;
}

.rain{
  margin-top:9px;
  font-size:13px;
  color:#9edbff;
}

.snow{
  margin-top:4px;
  font-size:13px;
  color:#e8f8ff;
}

.loading{
  text-align:center;
  padding:25px;
  opacity:.8;
}

.error{
  background:#812525;
  border-radius:12px;
  padding:15px;
}

#weatherMap{
  width:100%;
  height:350px;
  margin-top:15px;
  border-radius:18px;
  overflow:hidden;
}

footer{
  text-align:center;
  padding:30px;
  opacity:.6;
  font-size:13px;
}

</style>
</head>

<body>

<header>

<h1>🌦️ Greece Weather</h1>

<p>Πρόγνωση καιρού για όλο τον κόσμο</p>

</header>


<div class="container">


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


<div class="section-title">
Μεγάλες πόλεις
</div>

<div class="city-buttons">

<button data-name="Αθήνα" data-lat="37.9838" data-lon="23.7275">Αθήνα</button>
<button data-name="Θεσσαλονίκη" data-lat="40.6401" data-lon="22.9444">Θεσσαλονίκη</button>
<button data-name="Πάτρα" data-lat="38.2466" data-lon="21.7346">Πάτρα</button>
<button data-name="Ηράκλειο" data-lat="35.3387" data-lon="25.1442">Ηράκλειο</button>
<button data-name="Λάρισα" data-lat="39.6390" data-lon="22.4191">Λάρισα</button>
<button data-name="Βόλος" data-lat="39.3610" data-lon="22.9425">Βόλος</button>
<button data-name="Ιωάννινα" data-lat="39.6650" data-lon="20.8537">Ιωάννινα</button>
<button data-name="Καβάλα" data-lat="40.9396" data-lon="24.4018">Καβάλα</button>
<button data-name="Ρόδος" data-lat="36.4349" data-lon="28.2176">Ρόδος</button>
<button data-name="Χανιά" data-lat="35.5138" data-lon="24.0180">Χανιά</button>

</div>


<div class="section-title">
Άλλες περιοχές
</div>

<div class="city-buttons">

<button data-name="Κοζάνη" data-lat="40.3007" data-lon="21.7889">Κοζάνη</button>
<button data-name="Τρίκαλα" data-lat="39.5556" data-lon="21.7675">Τρίκαλα</button>
<button data-name="Σέρρες" data-lat="41.0856" data-lon="23.5483">Σέρρες</button>
<button data-name="Αλεξανδρούπολη" data-lat="40.8457" data-lon="25.8739">Αλεξανδρούπολη</button>
<button data-name="Κατερίνη" data-lat="40.2726" data-lon="22.5025">Κατερίνη</button>
<button data-name="Λαμία" data-lat="38.9000" data-lon="22.4340">Λαμία</button>
<button data-name="Χαλκίδα" data-lat="38.4635" data-lon="23.5994">Χαλκίδα</button>
<button data-name="Καλαμάτα" data-lat="37.0390" data-lon="22.1142">Καλαμάτα</button>
<button data-name="Μυτιλήνη" data-lat="39.1067" data-lon="26.5547">Μυτιλήνη</button>
<button data-name="Κόρινθος" data-lat="37.9386" data-lon="22.9322">Κόρινθος</button>

</div>


<div class="current">

<div class="city-name" id="cityName">
Θεσσαλονίκη
</div>

<div class="temp" id="currentTemp">
--
</div>

<div class="status" id="currentStatus">
Φόρτωση...
</div>

</div>


<div class="section-title">
15ήμερη πρόγνωση
</div>

<div id="forecast" class="forecast">

<div class="loading">
Φόρτωση πρόγνωσης...
</div>

</div>


<div class="section-title">
Τοποθεσία
</div>

<div id="weatherMap"></div>

</div>


<footer>
Δεδομένα: Open-Meteo / ECMWF
</footer>


<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

/* =====================================
   ΕΠΙΛΕΓΜΕΝΗ ΤΟΠΟΘΕΣΙΑ
===================================== */

let selectedCity = {
  name:"Θεσσαλονίκη",
  lat:40.6401,
  lon:22.9444
};


/* =====================================
   ΧΑΡΤΗΣ
===================================== */

let map;
let marker;

function startMap(){

  map = L.map("weatherMap").setView(
    [selectedCity.lat,selectedCity.lon],
    9
  );

  L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
      maxZoom:18,
      attribution:"© OpenStreetMap"
    }
  ).addTo(map);

  marker = L.marker([
    selectedCity.lat,
    selectedCity.lon
  ])
  .addTo(map)
  .bindPopup(selectedCity.name)
  .openPopup();
}


function updateMap(){

  marker
  .setLatLng([
    selectedCity.lat,
    selectedCity.lon
  ])
  .bindPopup(selectedCity.name)
  .openPopup();

  map.setView([
    selectedCity.lat,
    selectedCity.lon
  ],10);
}


/* =====================================
   ΕΠΙΛΟΓΗ ΠΟΛΗΣ
===================================== */

function selectCity(name,lat,lon){

  selectedCity = {
    name:name,
    lat:Number(lat),
    lon:Number(lon)
  };

  document.getElementById("cityName")
  .textContent=name;

  updateMap();

  loadCurrentWeather();

  loadForecast();
}


/* =====================================
   ΚΟΥΜΠΙΑ
===================================== */

document
.querySelectorAll(".city-buttons button")
.forEach(button=>{

  button.addEventListener("click",()=>{

    selectCity(
      button.dataset.name,
      button.dataset.lat,
      button.dataset.lon
    );

  });

});


/* =====================================
   CURRENT WEATHER
===================================== */

async function loadCurrentWeather(){

  const temp =
    document.getElementById("currentTemp");

  const status =
    document.getElementById("currentStatus");

  temp.textContent="--";
  status.textContent="Φόρτωση...";

  const url =
    "https://api.open-meteo.com/v1/forecast"+
    "?latitude="+selectedCity.lat+
    "&longitude="+selectedCity.lon+
    "&current=temperature_2m,weather_code"+
    "&timezone=auto";

  try{

    const response =
      await fetch(url,{cache:"no-store"});

    if(!response.ok)
      throw new Error("Current weather error");

    const data =
      await response.json();

    temp.textContent =
      Math.round(
        data.current.temperature_2m
      )+"°C";

    const weather =
      weatherFromCode(
        data.current.weather_code
      );

    status.textContent =
      weather.icon+" "+weather.text;

  }
  catch(error){

    console.error(error);

    status.textContent =
      "Δεν ήταν δυνατή η φόρτωση.";

  }
}


/* =====================================
   WMO WEATHER CODES
===================================== */

function weatherFromCode(code){

  switch(Number(code)){

    case 0:
      return {
        icon:"☀️",
        text:"Αίθριος"
      };

    case 1:
      return {
        icon:"🌤️",
        text:"Κυρίως αίθριος"
      };

    case 2:
      return {
        icon:"⛅",
        text:"Μερική συννεφιά"
      };

    case 3:
      return {
        icon:"☁️",
        text:"Συννεφιά"
      };

    case 45:
      return {
        icon:"🌫️",
        text:"Ομίχλη"
      };

    case 48:
      return {
        icon:"🌫️",
        text:"Παγωμένη ομίχλη"
      };

    case 51:
      return {
        icon:"🌦️",
        text:"Ελαφρύ ψιλόβροχο"
      };

    case 53:
      return {
        icon:"🌦️",
        text:"Ψιλόβροχο"
      };

    case 55:
      return {
        icon:"🌧️",
        text:"Ισχυρό ψιλόβροχο"
      };

    case 56:
      return {
        icon:"🌧️",
        text:"Ελαφρύ παγωμένο ψιλόβροχο"
      };

    case 57:
      return {
        icon:"🌧️",
        text:"Ισχυρό παγωμένο ψιλόβροχο"
      };

    case 61:
      return {
        icon:"🌦️",
        text:"Ελαφριά βροχή"
      };

    case 63:
      return {
        icon:"🌧️",
        text:"Βροχή"
      };

    case 65:
      return {
        icon:"🌧️",
        text:"Ισχυρή βροχή"
      };

    case 66:
      return {
        icon:"🌧️",
        text:"Ελαφριά παγωμένη βροχή"
      };

    case 67:
      return {
        icon:"🌧️",
        text:"Ισχυρή παγωμένη βροχή"
      };

    case 71:
      return {
        icon:"🌨️",
        text:"Ελαφριά χιονόπτωση"
      };

    case 73:
      return {
        icon:"❄️",
        text:"Χιονόπτωση"
      };

    case 75:
      return {
        icon:"❄️",
        text:"Ισχυρή χιονόπτωση"
      };

    case 77:
      return {
        icon:"❄️",
        text:"Κόκκοι χιονιού"
      };

    case 80:
      return {
        icon:"🌦️",
        text:"Ελαφριές μπόρες"
      };

    case 81:
      return {
        icon:"🌧️",
        text:"Μπόρες"
      };

    case 82:
      return {
        icon:"🌧️",
        text:"Ισχυρές μπόρες"
      };

    case 85:
      return {
        icon:"🌨️",
        text:"Ελαφριές μπόρες χιονιού"
      };

    case 86:
      return {
        icon:"❄️",
        text:"Ισχυρές μπόρες χιονιού"
      };

    case 95:
      return {
        icon:"⛈️",
        text:"Καταιγίδα"
      };

    case 96:
      return {
        icon:"⛈️",
        text:"Καταιγίδα με χαλάζι"
      };

    case 99:
      return {
        icon:"⛈️",
        text:"Ισχυρή καταιγίδα με χαλάζι"
      };

    default:
      return {
        icon:"🌤️",
        text:"Μεταβλητός καιρός"
      };

  }
}


/* =====================================
   MODEL DATA
===================================== */

async function getModelForecast(model){

  const url =
    "https://api.open-meteo.com/v1/forecast"+
    "?latitude="+selectedCity.lat+
    "&longitude="+selectedCity.lon+
    "&models="+model+
    "&daily="+
    "temperature_2m_max,"+
    "temperature_2m_min,"+
    "precipitation_sum,"+
    "rain_sum,"+
    "snowfall_sum,"+
    "weather_code"+
    "&forecast_days=15"+
    "&timezone=auto";

  const response =
    await fetch(url,{cache:"no-store"});

  if(!response.ok)
    throw new Error(model+" error");

  const data =
    await response.json();

  if(
    data.error ||
    !data.daily ||
    !data.daily.time
  ){

    throw new Error(
      model+" returned no data"
    );

  }

  return data.daily;
}


/* =====================================
   15ΗΜΕΡΗ ΠΡΟΓΝΩΣΗ
===================================== */

async function loadForecast(){

  const box =
    document.getElementById("forecast");

  box.innerHTML =
    '<div class="loading">Φόρτωση 15ήμερης πρόγνωσης...</div>';

  try{

    const [ifs,aifs] =
      await Promise.all([

        getModelForecast(
          "ecmwf_ifs025"
        ),

        getModelForecast(
          "ecmwf_aifs025"
        )

      ]);


    const days =
      Math.min(
        15,
        ifs.time.length,
        aifs.time.length
      );


    let html="";


    for(let i=0;i<days;i++){

      /*
       * Θερμοκρασία:
       * μέσος όρος των δύο μοντέλων
       */

      const maxTemp =
        (
          Number(ifs.temperature_2m_max[i])+
          Number(aifs.temperature_2m_max[i])
        )/2;

      const minTemp =
        (
          Number(ifs.temperature_2m_min[i])+
          Number(aifs.temperature_2m_min[i])
        )/2;


      /*
       * ΥΕΤΟΣ:
       * εμφανίζουμε τον μέσο όρο
       * των πραγματικών τιμών
       */

      const rain =
        (
          Number(ifs.rain_sum[i])+
          Number(aifs.rain_sum[i])
        )/2;


      const snow =
        (
          Number(ifs.snowfall_sum[i])+
          Number(aifs.snowfall_sum[i])
        )/2;


      /*
       * WEATHER CODE:
       *
       * ΔΕΝ κατασκευάζουμε δικό μας code.
       *
       * Χρησιμοποιούμε τον κωδικό
       * που δίνει το κάθε μοντέλο.
       *
       * Για την εμφάνιση επιλέγουμε
       * τον κωδικό με το μεγαλύτερο
       * severity.
       */

      const codeIFS =
        Number(ifs.weather_code[i]);

      const codeAIFS =
        Number(aifs.weather_code[i]);


      /*
       * Αν υπάρχει πραγματική
       * χιονόπτωση από κάποιο μοντέλο,
       * δείχνουμε χιονική κατάσταση
       * μόνο όταν ο κωδικός του μοντέλου
       * είναι επίσης χιονικός.
       */

      const snowCodes =
        [71,73,75,77,85,86];


      let finalCode;


      const ifsSnow =
        snowCodes.includes(codeIFS);

      const aifsSnow =
        snowCodes.includes(codeAIFS);


      if(ifsSnow && aifsSnow){

        /*
         * Και τα δύο μοντέλα συμφωνούν
         * για χιόνι.
         */

        finalCode =
          codeIFS >= codeAIFS
          ? codeIFS
          : codeAIFS;

      }

      else if(ifsSnow && snow > 0){

        finalCode=codeIFS;

      }

      else if(aifsSnow && snow > 0){

        finalCode=codeAIFS;

      }

      else{

        /*
         * Καμία χιονική ένδειξη.
         * Κρατάμε τον κωδικό του μοντέλου
         * με τη μεγαλύτερη κατηγορία WMO.
         */

        finalCode =
          Math.max(
            codeIFS,
            codeAIFS
          );

      }


      /*
       * ΗΜΕΡΟΜΗΝΙΑ
       */

      const date =
        new Date(
          ifs.time[i]+"T12:00:00"
        );

      const dateText =
        date.toLocaleDateString(
          "el-GR",
          {
            weekday:"short",
            day:"numeric",
            month:"short"
          }
        );


      /*
       * ΣΥΜΒΟΛΟ
       */

      const weather =
        weatherFromCode(finalCode);


      /*
       * CARD
       */

      html += `

      <div class="day">

        <div class="day-date">
          ${dateText}
        </div>

        <div class="weather-icon">
          ${weather.icon}
        </div>

        <div class="weather-text">
          ${weather.text}
        </div>

        <div class="max">
          ${Math.round(maxTemp)}°C
        </div>

        <div class="min">
          Ελάχιστη ${Math.round(minTemp)}°C
        </div>

        <div class="rain">
          🌧️ Βροχή: ${rain.toFixed(1)} mm
        </div>

        <div class="snow">
          ❄️ Χιόνι: ${snow.toFixed(1)} cm
        </div>

      </div>

      `;

    }


    box.innerHTML=html;

  }

  catch(error){

    console.error(
      "FORECAST ERROR:",
      error
    );

    box.innerHTML=`

      <div class="error">

        ❌ Δεν φορτώθηκε η πρόγνωση.

        <br><br>

        Γίνεται νέα προσπάθεια...

      </div>

    `;

    setTimeout(
      loadForecast,
      5000
    );

  }

}


/* =====================================
   ΑΝΑΖΗΤΗΣΗ
===================================== */

async function searchPlace(){

  const input =
    document.getElementById(
      "searchInput"
    );

  const query =
    input.value.trim();

  if(!query)
    return;


  const button =
    document.getElementById(
      "searchButton"
    );

  button.textContent="...";


  try{

    const url =
      "https://geocoding-api.open-meteo.com/v1/search"+
      "?name="+encodeURIComponent(query)+
      "&count=1"+
      "&language=el"+
      "&format=json";


    const response =
      await fetch(
        url,
        {cache:"no-store"}
      );


    if(!response.ok)
      throw new Error("Search error");


    const data =
      await response.json();


    if(
      !data.results ||
      data.results.length===0
    ){

      alert(
        "Δεν βρέθηκε η περιοχή."
      );

      return;

    }


    const place =
      data.results[0];


    selectCity(
      place.name,
      place.latitude,
      place.longitude
    );


    input.value="";

  }

  catch(error){

    console.error(error);

    alert(
      "Δεν ήταν δυνατή η αναζήτηση αυτή τη στιγμή."
    );

  }

  finally{

    button.textContent=
      "Αναζήτηση";

  }

}


/* =====================================
   SEARCH BUTTON
===================================== */

document
.getElementById("searchButton")
.addEventListener(
  "click",
  searchPlace
);


/* =====================================
   ENTER
===================================== */

document
.getElementById("searchInput")
.addEventListener(
  "keydown",
  event=>{

    if(event.key==="Enter"){
      searchPlace();
    }

  }
);


/* =====================================
   START
===================================== */

startMap();

loadCurrentWeather();

loadForecast();

</script>

</body>
</html>
