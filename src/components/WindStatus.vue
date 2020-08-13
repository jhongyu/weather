<template>
  <div class="wrapper">
    <div class="title">
      <p>Wind status</p>
    </div>
    <div class="content">
      <p>{{ speed }}mph</p>
    </div>
    <div class="status">
      <p>{{ weather.consolidated_weather[0].wind_direction_compass }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'windstatus',
  props: ['weather'],
  computed: {
    speed() {
      return Math.round(this.weather.consolidated_weather[0].wind_speed);
    }
  }
}
</script>

<style>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: var(--card-background-color);
  border: 1px solid var(--card-background-color);
  padding: 5px 20px;
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
