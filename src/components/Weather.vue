<template>
  <div class="weather" v-on:unit-changed="changeUnit">
    <div class="convertor">
      <convertor unit="℃"></convertor>
      <convertor unit="℉"></convertor>
    </div>
    <div class="card">
      <weather-card
        :key="item.id"
        v-for="item in weather.consolidated_weather"
        :todayWeather="item"
      ></weather-card>
    </div>
  </div>
</template>

<script>
import Convertor from './Convertor.vue'
import WeatherCard from './WeatherCard.vue'

export default {
  name: 'weather',
  components: {
    Convertor,
    WeatherCard
  },
  props: ['weather'],
  data() {
    return {
      unit: ''
    }
  },
  methods: {
    changeUnit: function (unit) {
      this.unit = unit;
      console.log(unit);
    }
  }
}
</script>

<style>
.weather {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.convertor {
  flex: 1.5;
}

.card {
  flex: 2;
  display: flex;
}
</style>
