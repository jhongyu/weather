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
  name: 'SideBar',
  props: ['weatherData']
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
}

.weather {
  flex: 5;
}

.footer {
  flex: 1;
}
</style>
