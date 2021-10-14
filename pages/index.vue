<template>
  <b-container class="m-auto rounded">
    <b-row class="bg-white">
      <b-col sm="12">
        <h3 class="text-center">{{ weather.name }}</h3>
      </b-col>
      <b-col sm="12">
        <p class="text-center">{{ new Date().toGMTString() }}</p>
      </b-col>
      <b-col>
        <h5>{{ weather.weather }}</h5>
        <img
          :src="`https://openweathermap.org/img/w/${weather.weather[0].icon}.png`"
          alt=""
        />
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
            id: 802,
            main: 'Clouds',
            description: 'scattered clouds',
            icon: '03d',
          },
        ],
        base: 'stations',
        main: {
          temp: 295.28,
          feels_like: 294.25,
          temp_min: 295.28,
          temp_max: 295.28,
          pressure: 1006,
          humidity: 27,
          sea_level: 1006,
          grnd_level: 702,
        },
        visibility: 10000,
        wind: {
          speed: 1.61,
          deg: 104,
          gust: 4.19,
        },
        clouds: {
          all: 48,
        },
        dt: 1634232749,
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
  background-color: whitesmoke;
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 100vw;
  width: 100%;
  height: 100vh;
}
.bg-white {
  background-color: white;
}
</style>
