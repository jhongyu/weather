<template>
  <div class="container">
    <div class="header">
      <button class="search">Search for places</button>
    </div>
    <div class="weather">
      <div class="img"></div>
      <div class="temperature" v-if="weatherData">
        {{ weatherData.consolidated_weather[0].the_temp }}
      </div>
      <div class="description" v-if="weatherData">
        {{ weatherData.consolidated_weather[0].weather_state_name }}
      </div>
    </div>
    <div class="footer">
      <div class="date">Today · {{ weatherData.time }}</div>
      <div class="position">{{ weatherData.title }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weatherData: ''
    }
  },
  beforeCreate() {
    const that = this;
    const options = {
      enableHighAccuracy: true,
      timeout: 5000,
      maximumAge: 0
    };

    function success(pos) {
      const coords = pos.coords;
      that.getWeatherData(coords.latitude, coords.longitude);
    }

    function error(err) {
      console.warn(`ERROR(${err.code}): ${err.message}`)
    }

    navigator.geolocation.getCurrentPosition(success, error, options);
  },
  methods: {
    async getWeatherData(latitude, longitude) {
      const cors = "https://cors-anywhere.herokuapp.com/";
      let location = await (await fetch(`${cors}https://www.metaweather.com/api/location/search/?lattlong=${latitude},${longitude}`)).json();
      let data = await (await fetch(`${cors}https://www.metaweather.com/api/location/${location[0].woeid}`)).json();
      this.weatherData = data;
    }
  }
}
</script>
