<template>
  <div class="wrapper">
    <div class="title">
      <p>Visibility</p>
    </div>
    <div class="content">
      <p>{{ visibility }}miles</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'visibility',
  props: ['weather'],
  computed: {
    visibility() {
      return Math.round(this.weather.consolidated_weather[0].visibility * 10) / 10;
    }
  }
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
