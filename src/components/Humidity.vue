<template>
  <div class="wrapper">
    <div class="title">
      <p>Humidity</p>
    </div>
    <div class="content">
      <p>{{ weather.consolidated_weather[0].humidity }}%</p>
    </div>
    <div class="status"></div>
  </div>
</template>

<script>
export default {
  name: 'humidity',
  props: ['weather']
}
</script>

<style>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.title {
  flex: 1;
  display: flex;
  align-items: center;
}

.content {
  flex: 1;
  display: flex;
  align-items: center;
}

.status {
  flex: 1;
  display: flex;
  align-items: center;
}
</style>
