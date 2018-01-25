<template>
  <div>
    <h1>Weather {{msg}}</h1>
    <ul>
      <li v-for="(day, key) in weatherData" :key="key">
        [ {{day.dt_txt}} ]
        <br>
        {{ day.main.temp }} C
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'GridView',
  data() {
    return {
      msg: 'Grid',
    };
  },
  props: ['weatherData'],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  ul {
    columns: 2;
  }
</style>
