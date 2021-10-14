<template>
  <b-container class="mx-auto my-5 rounded">
    <b-row class="p-3">
      <b-col md="12" class="my-3">
        <WeatherCard v-if="!error && weather" :weather="weather"></WeatherCard>
        <h5 v-else class="text-danger text-center w-100">
          {{ message }}
        </h5>
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
      lon: 0,
      error: false,
      message: '',
      weather: '',
    }
  },
  async created() {
    if (process.browser) {
      if ('geolocation' in navigator) {
        const { state } = await navigator.permissions.query({
          name: 'geolocation',
        })
        if (state === 'denied') {
          this.error = true
          this.message =
            'No podemos darte el clima de tu ciudad si bloqueas los permisos :('
        } else {
          navigator.geolocation.getCurrentPosition((position) => {
            this.lat = position.coords.latitude
            this.lon = position.coords.longitude
            this.getWeather()
          })
        }
        /* geolocation is available */
      } else {
        this.error = true
        this.message = 'Tu navagador no soporta la geolocacion :('
        /* geolocation IS NOT available */
      }
    }
  },
  methods: {
    async getWeather() {
      try {
        const key = process.env.APIKEY
        const { data } = await this.$axios.get(
          `https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}&lon=${this.lon}&appid=${key}&units=metric`
        )
        this.weather = data
      } catch (error) {
        this.error = true
        this.message = 'Ocurrio un error '
        console.log(error)
      }
    },
  },
})
</script>
<style>
body {
  background-color: #e7fbff;
  max-width: 100vw;
  width: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Open Sans, sans-serif;
}
.bg-white {
  background-color: white;
}
</style>
