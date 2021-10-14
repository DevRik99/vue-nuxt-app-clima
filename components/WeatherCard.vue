<template>
  <b-row class="weather-card weather-card-info p-3 mx-auto overflow-hidden">
    <b-col
      sm="12"
      md="4"
      lg="3"
      class="weather-description temperature-container my-3"
    >
      <p class="temperature-title">Temperatura</p>
      <h1 class="temperature-temperature">{{ weather.main.temp }}°</h1>
      <p class="temperature-min mx-1">Min: {{ weather.main.temp_min }}°</p>
      <p class="temperature-max mx-1">Max: {{ weather.main.temp_max }}°</p>
    </b-col>
    <b-col sm="12" md="4" lg="6" class="weather-description my-3">
      <p class="my-2 my-md-0 text-center w-100 font-weight-bold">
        {{
          weather.dt
            ? $dayjs.unix(weather.dt).format('dddd, MMMM D, YYYY h:mm A')
            : $dayjs(new Date()).format('MMMM D, YYYY')
        }}
      </p>
      <h5 class="my-2 my-md-0">
        <i class="bx bxs-map"></i>
        {{ weather.name || 'En algun lugar de la tierra' }}
      </h5>
      <p class="my-2 my-md-0" v-if="weather.sys.sunrise">
        Amanecer :
        <WeatherTime
          :time="weather.sys.sunrise"
          class="d-inline-block font-weight-bold"
        ></WeatherTime>
      </p>
      <p class="my-2 my-md-0" v-if="weather.sys.sunset">
        puesta de sol :
        <WeatherTime
          :time="weather.sys.sunset"
          class="d-inline-block font-weight-bold"
        ></WeatherTime>
      </p>
      <!-- <img
        :src="`https://flagcdn.com/16x12/${weather.sys.country.toLowerCase()}.png`"
        :srcset="`https://flagcdn.com/32x24/${weather.sys.country.toLowerCase()}.png 2x,https://flagcdn.com/48x36/${weather.sys.country.toLowerCase()}.png 3x`"
        width="16"
        height="12"
        :alt="weather.sys.country"
      />-->
    </b-col>
    <b-col sm="12" md="4" lg="3" class="weather-description-icon my-3">
      <WeatherIcon :icon="getIcon(weather.weather).icon"></WeatherIcon>
      <h5 class="text-center">{{ getIcon(weather.weather).title }}</h5>
    </b-col>
  </b-row>
</template>

<script>
export default {
  props: {
    weather: {
      type: Object,
      // eslint-disable-next-line vue/require-valid-default-prop
      default: {},
      required: true,
    },
  },
  methods: {
    getIcon(weather) {
      const icon = weather[0].icon.replace(/n/g, 'd')
      const iconsList = {
        '01d': { icon: 'sunny', title: 'cielo despejado' },
        '02d': { icon: 'cloudy', title: 'pocas nubes' },
        '03d': { icon: 'cloudy', title: 'nubes dispersas' },
        '04d': { icon: 'cloudy-dark', title: 'nubes nubladas' },
        '09d': { icon: 'rainy', title: 'lluvia' },
        '10d': { icon: 'rainy', title: 'lluvia' },
        '11d': { icon: 'storm', title: 'Tormenta' },
        '13d': { icon: 'flurries', title: 'Nieve' },
        '50d': { icon: 'cloudy', title: 'Neblina' },
      }
      return iconsList[icon]
    },
  },
}
</script>

<style lang="css" scoped>
.weather-title,
.weather-description {
  color: white;
}
.weather-card {
  border-radius: 15px;
  text-transform: capitalize;
  width: 98%;
}

.weather-card-info {
  background-image: linear-gradient(90deg, #1b92ff, #5bb6ff);
}
.weather-description {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  flex-direction: column;
}
.weather-description-icon {
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.temperature-container {
  display: grid;
  gap: 8px 0;
  justify-content: center;
  align-content: space-between;
  text-align: center;
  grid-template-areas:
    'title title'
    'temperature temperature'
    'min max';
}
.temperature-title {
  grid-area: title;
}
.temperature-temperature {
  grid-area: temperature;
}
.temperature-max {
  grid-area: max;
}
.temperature-min {
  grid-area: min;
}
.temperature-container ::after {
  content: '';
  display: block;
  position: absolute;
  width: 2px;
  height: 100%;
  border-radius: 1px;
  top: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.1);
}
p,
h1,
h5 {
  margin-top: 0;
  margin-bottom: 0;
}
</style>
