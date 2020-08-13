<template>
  <div class="wrapper">
    <div class="title">
      <p>Visibility</p>
    </div>
    <div class="content">
      <p>{{ weather.consolidated_weather[0].visibility }}miles</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'visibility',
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
