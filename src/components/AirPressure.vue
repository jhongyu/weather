<template>
  <div class="wrapper">
    <div class="title">
      <p>Air Pressure</p>
    </div>
    <div class="content">
      <p>{{ weather.consolidated_weather[0].air_pressure }}mb</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'airpressure',
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
</style>
