<template>
    <div class="container">
        <div class="header">
            <button class="search">Search for places</button>
        </div>
        <div class="weather">
            <div class="img"></div>
            <div class="temperature">
                {{ weatherData.consolidated_weather[0].the_temp }}
            </div>
            <div class="description">
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
    getWeatherData(latitude, longitude) {
      const cors = "https://cors-anywhere.herokuapp.com/";
      fetch(`${cors}https://www.metaweather.com/api/location/search/?lattlong=${latitude},${longitude}`).then(response => {
        return response.json();
      }).then(data => {
        fetch(`${cors}https://www.metaweather.com/api/location/${data[0].woeid}`).then(data => {
          this.weatherData = data;
          console.log(this.weatherData,data);
        })
      })
    }
  }
}
</script>
