<template>
  <div class="wrapper">
    <div class="title">
      <p>Wind status</p>
    </div>
    <div class="content">
      <p>{{ weather.consolidated_weather[0].wind_speed }}mph</p>
    </div>
    <div class="status">
      <p>{{ weather.consolidated_weather[0].wind_direction_compass }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'windstatus',
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
