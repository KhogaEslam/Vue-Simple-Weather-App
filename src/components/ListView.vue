<template>
  <div>
    <h1>Weather {{msg}}</h1>
    <ul>
      <li v-for="(day, key) in weatherData" :key="key">
        [ {{day.dt_txt}} ] - {{ day.main.temp }} C
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ListView',
  data() {
    return {
      msg: 'List',
    };
  },
  props: ['weatherData'],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
