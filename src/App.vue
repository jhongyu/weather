<template>
  <div id="app" v-if="data">
    <div class="sidebar">
      <side-bar :weatherData="data"></side-bar>
    </div>
    <div class="content">
      <div class="top">
        <weather :weather="data"></weather>
      </div>
      <div class="down">
        <h2>Today's Highlights</h2>
        <div class="highlights">
          <wind-status :weather="data"></wind-status>
          <humidity :weather="data"></humidity>
          <visibility :weather="data"></visibility>
          <air-pressure :weather="data"></air-pressure>
        </div>
      </div>
      <div class="footer">
        <p>纪宏宇 @ DevChallenges.io</p>
      </div>
    </div>
  </div>
</template>

<script>
import SideBar from './components/SideBar.vue'
import Weather from './components/Weather.vue'
import WindStatus from './components/WindStatus.vue'
import Humidity from './components/Humidity.vue'
import Visibility from './components/Visibility.vue'
import AirPressure from './components/AirPressure.vue'

export default {
  name: 'App',
  components: {
    SideBar,
    Weather,
    WindStatus,
    Humidity,
    Visibility,
    AirPressure
  },
  data() {
    return {
      data: ''
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
      this.data = data;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
}

#app .sidebar {
  flex: 1;
}

#app .content {
  flex: 2;
  display: flex;
  flex-direction: column;
}

.content .top {
  flex: 3;
}

.content .down {
  flex: 6;
  display: flex;
  flex-direction: column;
}

.down h2 {
  flex: 1;
}

.down .highlights {
  flex: 9;
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.content .footer {
  flex: 1;
}
</style>
