<template>
  <div class="weather">
    <div class="convertor">
      <convertor unit="℃" @unit-changed="changeUnit"></convertor>
      <convertor unit="℉" @unit-changed="changeUnit"></convertor>
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
  width: 80%;
  margin-bottom: 30px;
  display: flex;
  justify-content: flex-end;
}

.card {
  width: 80%;
  flex: 2;
  display: flex;
  justify-content: space-between;
}
</style>
