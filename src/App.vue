<template>
  <div id="app" v-if="data">
    <div class="sidebar">
      <side-bar :weatherData="data" @get-location="getLocation"></side-bar>
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
  created() {
    this.getLocation();
  },
  methods: {
    async getWeatherData(latitude, longitude) {
      const cors = "https://cors-anywhere.herokuapp.com/";
      let location = await (await fetch(`${cors}https://www.metaweather.com/api/location/search/?lattlong=${latitude},${longitude}`)).json();
      let data = await (await fetch(`${cors}https://www.metaweather.com/api/location/${location[0].woeid}`)).json();
      this.data = data;
    },
    getLocation() {
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
  color: var(--text-color);
  display: flex;
  width: 100%;
  height: 100%;
}

#app .sidebar {
  flex: 1;
  background-color: var(--card-background-color);
}

#app > .content {
  flex: 2;
  display: flex;
  flex-direction: column;
  background-color: var(--main-background-color);
}

.content .top {
  width: 100%;
  flex: 3;
  padding-top: 30px;
}

.content .down {
  width: 100%;
  flex: 6;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.down h2 {
  flex: 1;
}

.down .highlights {
  flex: 9;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  width: 80%;
}

.content .footer {
  width: 100%;
  flex: 1;
}

.content .footer p {
  line-height: 94.5px;
  margin: 0 auto;
}
</style>
