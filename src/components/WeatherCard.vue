<template>
  <div id="card">
    <div class="date">
      <p>{{ date }}</p>
    </div>
    <div class="img">
      <img :src="path" :alt="weatherstate" />
    </div>
    <div class="temperature">
      <span class="max">{{ maxtemp }}℃</span>
      <span class="min">{{ mintemp }}℃</span>
    </div>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
  name: 'weatherCard',
  props: ['todayWeather'],
  data() {
    return {
      weatherstate: this.todayWeather.weather_state_abbr,
    }
  },
  computed: {
    maxtemp() {
      return Math.round(this.todayWeather.max_temp)
    },
    mintemp() {
      return Math.round(this.todayWeather.min_temp)
    },
    date() {
      return dayjs(this.todayWeather.applicable_date).format('ddd, D MMM');
    },
    path() {
      return 'https://www.metaweather.com/static/img/weather/' + this.weatherstate + '.svg';
    }
  }
}
</script>

<style>
#card {
  display: flex;
  flex-direction: column;
  background-color: var(--card-background-color);
  border: 1px solid var(--card-background-color);
  padding: 5px 20px;
}

#card .date {
  flex: 1;
  display: flex;
  align-items: center;
}

#card .img {
  flex: 3;
  display: flex;
  align-items: center;
}

#card .temperature {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
