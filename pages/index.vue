<template>
  <b-container class="mx-auto my-5 rounded">
    <b-row class="p-3">
      <b-col md="12">
        <WeatherCard :weather="weather"></WeatherCard>
      </b-col>
    </b-row>
  </b-container>
</template>
<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      lat: 0,
      long: 0,
      weather: {
        coord: {
          lon: -75.2124,
          lat: -12.0947,
        },
        weather: [
          {
            id: 804,
            main: 'Clouds',
            description: 'overcast clouds',
            icon: '04d',
          },
        ],
        base: 'stations',
        main: {
          temp: 12.13,
          feels_like: 11.49,
          temp_min: 12.13,
          temp_max: 12.13,
          pressure: 1014,
          humidity: 80,
          sea_level: 1014,
          grnd_level: 699,
        },
        visibility: 10000,
        wind: {
          speed: 5.18,
          deg: 119,
          gust: 5.69,
        },
        clouds: {
          all: 90,
        },
        dt: 1634247943,
        sys: {
          country: 'PE',
          sunrise: 1634207761,
          sunset: 1634252233,
        },
        timezone: -18000,
        id: 3939459,
        name: 'Huancayo',
        cod: 200,
      },
    }
  },
  created() {
    if (process.browser) {
      if ('geolocation' in navigator) {
        /* geolocation is available */
        navigator.geolocation.getCurrentPosition((position) => {
          this.lat = position.coords.latitude
          this.long = position.coords.longitude
        })
      } else {
        /* geolocation IS NOT available */
      }
    }
  },
})
</script>
<style>
body {
  background-color: #e7fbff;
  max-width: 100vw;
  width: 100%;
  min-height: 100vh;
  font-family: Open Sans, sans-serif;
}
.bg-white {
  background-color: white;
}
</style>
