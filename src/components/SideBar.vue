<template>
  <div class="container">
    <div class="header">
      <button class="search">Search for places</button>
      <button class="locate" @click="$emit('get-location')">📡</button>
    </div>
    <div class="weather">
      <div class="img">
        <img
          :src="require('../assets/img/' + this.status + '.png')"
          :alt="status"
        />
      </div>
      <div class="temperature">{{ temp }}℃</div>
      <div class="description">
        {{ weatherData.consolidated_weather[0].weather_state_name }}
      </div>
    </div>
    <div class="footer">
      <div class="date">Today · {{ time }}</div>
      <div class="position">{{ weatherData.title }}</div>
    </div>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
  name: 'SideBar',
  props: ['weatherData'],
  data() {
    return {
      statusname: this.weatherData.consolidated_weather[0].weather_state_name,
    }
  },
  computed: {
    status() {
      return this.statusname.split(' ').join('');
    },
    temp() {
      return Math.round(this.weatherData.consolidated_weather[0].the_temp)
    },
    time() {
      return dayjs(this.weatherData.time).format('ddd, D MMM');
    }
  }
}
</script>

<style>
.container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.header {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
}

.header .search {
  background-color: var(--button-background-color);
  color: var(--text-color);
  justify-content: start;
  padding: 8px;
  border: 1px solid black;
  border-radius: 5px;
}

.header .locate {
  background-color: var(--button-background-color);
  justify-content: end;
  border-width: 0;
  border-radius: 45%;
  padding: 8px;
  width: 35px;
  height: 35px;
}

.weather {
  flex: 5;
  display: flex;
  flex-direction: column;
}

.weather .img {
  flex: 3;
  display: flex;
  align-items: center;
}

.weather .img img {
  max-width: 100%;
  min-width: 100%;
  margin: 0 auto;
}

.weather > .temperature {
  flex: 1;
  display: flex;
  align-items: center;
  font-size: 4rem;
}

.weather .description {
  flex: 1;
  display: flex;
  align-items: center;
  font-size: 2rem;
}

.footer {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.footer > * {
  flex: 1;
  align-items: center;
}
</style>
