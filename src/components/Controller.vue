<template>
  <div class="controller">
    <select name="country" @change="updateCities">
      <option v-for="(value, key) in countries" :key=key :value="key">{{value}}</option>
    </select>

    <select name="city" @change="fetchWeather">
      <option v-for="city in cities" :key=city :value="city">{{city}}</option>
    </select>

    <button id="change-view" v-on:click="changeViewMode(viewMode)">{{viewMode}}</button>
  </div>
</template>

<script>
export default {
  name: 'Controller',
  data() {
    return {
      viewMode: 'G',
      countries: {
        EG: 'Egypt',
        US: 'US',
        UK: 'UK',
      },
      cities: [
        'Alexandria',
        'Cairo',
        'Aswan',
      ],
    };
  },
  methods: {
    updateCities: function updateCities(event) {
      const country = event.target.value;
      let city = '';
      switch (country) {
        case 'Egypt':
          this.cities = [
            'Alexandria',
            'Cairo',
            'Aswan',
          ];
          city = 'Alexandria';
          break;
        case 'US':
          this.cities = [
            'Denver',
            'Omaha',
            'Reno',
          ];
          city = 'Denver';
          break;
        case 'UK':
          this.cities = [
            'London',
            'Newport',
            'Reading',
          ];
          city = 'London';
          break;
        default:
          break;
      }
      this.$emit('update-country', { country, city });
    },
    fetchWeather: function fetchWeather(event) {
      const city = event.target.value;
      this.$emit('update-city', city);
    },
    changeViewMode: function changeViewMode(mode) {
      this.viewMode = (mode === 'G') ? 'L' : 'G';
      this.$emit('update-mode', this.viewMode);
    },
  },

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
