<template>
  <div id="card">
    <div class="date">
      <p>{{ todayWeather.applicable_date }}</p>
    </div>
    <div class="img">
      <img src="" alt="" />
    </div>
    <div class="temperature">
      <p class="max">{{ todayWeather.max_temp }}</p>
      <p class="min">{{ todayWeather.min_temp }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'weatherCard',
  props: ['todayWeather']
}
</script>
