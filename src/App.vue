<template>
  <main id="app" v-bind:class="computeClass(computedClass)">
    <div class="search">
      <input type="text" class="searchbar" placeholder="Ort eingeben" v-model="query" @keypress="getData">
    </div>

    
    <div id="wrapper1" class="weather-wrapper" v-if="typeof(weather.main) != 'undefined'">
      <div class="location-box">
        <div class="location">{{ weather.name }}, {{ weather.sys.country }} </div>
        <div class="date"> {{ handleDate() }} </div>
      </div>

      <div class="weatherbox">
        <div class="temperature">{{ Math.round(weather.main.temp) }}°C</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
        <img src="" />
      </div>
    </div>

    <div class="wikipediaWrapper" v-if="typeof(weather.main) != 'undefined'">
      <Article ref="articleComponent"></Article>
    </div>
    

  </main>
</template>

<script>
import Article from './components/Article.vue'
export default {
  name: "App",

  components: {
    Article,
  },

  data () {
    return{
      api_key: '1f3e379d7b4cbb2bbb0527cb6b3a654b',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      url_base_icon: 'http://openweathermap.org/img/w/',  //&prop=extracts&format=json&exintro=1
      query:'',
      weather: {}
    }
  },

  methods: {

    //Fetch Weather & Wikipedia Data

    getData (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setWeather).then(() => {this.$refs.articleComponent.getArticle(this.query)});
        
        //this.getArticle();
        //this.$refs.articleComponent.reload();
      }
    },


    //set fetched weather as variable

    setWeather (results) {
      this.weather = results;
      this.weatherStatus = this.weather.weather[0].main;
    },

    //Date Handler -> Load and proccess date

    handleDate () {
      let date = new Date();
      let day = date.getDate();
      let month = date.getMonth() + 1;
      let year = date.getFullYear();

      if(day<10){
        day = '0' + day;
      }

      return `${day}.${month}.${year}`;
    },

    // coumpute main class, depending on temperature, to set background conditionally
    computeClass: function (classname){
      classname = 'default';
      let date = new Date();
      let hour = date.getHours();

      if(this.weather.main !== undefined){
        if (this.weather.main.temp > 14 && hour > 7 && hour < 18){
          classname = 'warm';
        }
        else if(this.weather.main.temp > 14){
          classname = 'warmnight'
        }
        else if(this.weather.main.temp < 15 && hour > 7 && hour < 18){
          classname = 'cold';
        }
        else if(this.weather.main.temp < 15){
          classname = 'coldnight';
        }
      }
      return classname;
    }
  }
}

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
  background-size: cover;
  background-position: bottom;
  transition: 0.6s;
}

#app.default {
  background: rgb(181,102,102);
  background: radial-gradient(circle, rgba(181,102,102,1) 0%, rgba(9,121,88,1) 35%, rgba(0,212,255,1) 100%);
}

#app.warm {
  background-image: url('./assets/warm.jpg');
}

#app.warmnight {
  background-image: url('./assets/warmnight.jpg');
}

#app.cold {
  background-image: url('./assets/cold.jpg');
}

#app.coldnight {
  background-image: url('./assets/coldnight.jpg');
}


main{
  text-align: center;
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

  color: whitesmoke;
}

.search .searchbar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.2);
  background-color: rgba(255 , 255, 255, 0.6);

  color: black;
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

#wrapper1 {
  display: inline-block;
  padding: 10px 25px;
  background-color: rgba(0 , 0, 0, 0.7);
  border-radius: 20px;
  margin: 30px 0px;

  box-shadow: 3px 4px rgba(0, 0, 0, 0.3);
}

.weatherbox {
  text-align: center;
}

.weatherbox .temperature {
  display: inline-block;
  padding: 10px 25px;
  color: whitesmoke;
  font-size: 80px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.2);
  background-color: rgba(255 , 255, 255, 0.25);
  border-radius: 20px;
  margin: 30px 0px;
}

.weatherbox .weather {
  color: whitesmoke;
  font-size: 47px;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.2);
}
</style>
