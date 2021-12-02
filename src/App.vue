<template>
  <main>
    <div class="search">
      <input type="text" class="searchbar" placeholder="Ort eingeben" v-model="query" @keypress="getData">
    </div>

    <div class="weather-wrapper" v-if="typeof weather.main != 'undefied'">
      <div class="location-box">
        <div class="location">{{ weather.name }}, {{weather.sys.country}}</div>
        <div class="date">Donnerstag 02.12.2021</div>
      </div>

      <div class="weatherbox">
        <div class="temperature">1°C</div>
        <div class="weather">Snow</div>
      </div>
    </div>
  </main>
</template>

<script>

export default {
  name: "App",
  data () {
    return{
      api_key: '1f3e379d7b4cbb2bbb0527cb6b3a654b',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather: {}
    }
  },
  methods: {
    getData (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setWeather);
      }
    },

    setWeather (results) {
      this.weather = results;
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'montserrat', sans-serif;
}

#app{
  background-image: url('./assets/cold.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.6s;
}

main{
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.2));
}

.search {
  width: 100%;
  margin-bottom: 30px;
}

.search .searchbar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.2);
  background-color: rgba(255, 255, 255, 0,5);
  border-radius: 15px;
  transition: 0.6s;
}

.search .searchbar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.2);
  background-color: rgba(255 , 255, 255, 0.6);
}

.location-box .location {
  color: whitesmoke;
  font-size: 35px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.2);
}

.location-box .date {
  color: whitesmoke;
  font-size: 25px;
  font-weight: 150;
  font-style: italic;
  text-align: center;
}

.weatherbox {
  text-align: center;
}

.weatherbox .temperature {
  display: inline-block;
  padding: 10px 25px;
  color: whitesmoke;
  font-size: 100px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.2);
  background-color: rgba(255 , 255, 255, 0.25);
  border-radius: 20px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.1);
}

.weatherbox .weather {
  color: whitesmoke;
  font-size: 47px;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.2);
}
</style>
