<template>
  <div class="sidebar">
    <section class="ctn" v-if="this.current">
      <WeatherInfo :icon="'wi-raindrops'" :title="'Humidité'" :value="this.current.main.humidity" :unit="'%'"></WeatherInfo>
      <WeatherInfo :icon="'wi-strong-wind'" :title="'Vit. vent'" :value="this.current.wind.speed * 3.6" :unit="'km/s'"></WeatherInfo>
    </section>
    <div class="sidebar--background"></div>
  </div>
</template>
<script>
import WeatherInfo from '../components/WeatherInfo'
export default {
  name: 'SideBar',
  components: {
    WeatherInfo
  },
  props: [
    'current'
  ]
}
</script>
