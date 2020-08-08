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
  beforeMount() {
    const that = this;
    const options = {
      enableHighAccuracy: true,
      timeout: 5000,
      maximumAge: 0
    };

    function success(pos) {
      const coord = pos.coords;
      that.getWeatherData(coord.latitude, coord.longitude);
    }

    function errer(err) {
      console.warn(`ERROR(${err.code}): ${err.message}`)
    }

    navigator.geolocation.getCurrentPosition(success, errer, options);
  },
  methods: {
    getWeatherData(latitude, longitude) {
      fetch(`https://www.metaweather.com/api/location/search/?lattlong=${latitude},${longitude}`).then(location => {
        fetch(`https://www.metaweather.com/api/location/${location.json().woeid}`).then(data => {
          this.weatherData = data.json();
        })
      })
    }
  }
}
</script>
