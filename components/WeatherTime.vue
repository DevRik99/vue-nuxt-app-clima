<template>
  <div>{{ timeParsed }}</div>
</template>

<script>
export default {
  props: {
    time: {
      type: Number,
      // eslint-disable-next-line vue/require-valid-default-prop
      default: 0,
      required: true,
    },
  },
  data() {
    return {
      timeParsed: 0,
    }
  },
  created() {
    this.parseTime()
    setInterval(() => this.parseTime(), 1000 * 1 * 60)
  },
  methods: {
    parseTime() {
      this.timeParsed = this.$dayjs.unix(this.time).fromNow()
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
  place-content: center;
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
</style>
