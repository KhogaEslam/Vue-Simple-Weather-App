<template>
  <div id="app">
    <img src="./assets/waether.jpg" width="300px">
    <Controller
    @update-mode="changeViewMode"
    @update-country="changeCountry"
    @update-city="changeCity" />

    <GridView v-if="viewMode !== 'G'" :weather-data="weatherData"/>
    <ListView v-if="viewMode !== 'L'" :weather-data="weatherData"/>
  </div>
</template>

<script>
import axios from 'axios';
import Controller from './components/Controller';
import GridView from './components/GridView';
import ListView from './components/ListView';

export default {
  name: 'App',
  data() {
    return {
      weatherData: [],
      errors: [],
      viewMode: 'G',
      country: 'Eg',
      city: 'Alexandria',
    };
  },
  components: {
    Controller,
    GridView,
    ListView,
  },
  methods: {
    changeViewMode: function changeViewMode(mode) {
      this.viewMode = mode;
    },
    changeCountry: function changeCountry(obj) {
      this.country = obj.country;
      this.city = obj.city;
      this.fetchWeather();
    },
    changeCity: function changeCity(city) {
      this.city = city;
      this.fetchWeather();
    },
    fetchWeather: function fetchWeather() {
      const APPID = 'a13a21def33c31deca8a9b39a632aa68';
      const city = this.city;
      const country = this.country;
      axios.get(`http://api.openweathermap.org/data/2.5/forecast?q=${city},${country}&appid=${APPID}&units=metric`)
        .then((response) => {
          this.weatherData = response.data.list;
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
  },
  created() {
    this.fetchWeather();
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul {
  list-style-type: none;
}
li {
  border: 1px solid;
}
</style>
