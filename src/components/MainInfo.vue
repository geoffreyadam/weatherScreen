<template>
  <div class="basic-info" v-if="this.current && this.conditionCodes">
    <i class="wi" :class="this.night ? this.conditionCodes[this.current.weather[0].id].iconDay : this.conditionCodes[this.current.weather[0].id].iconNight"></i>
    <h2>{{ this.current.weather[0].description.charAt(0).toUpperCase() + this.current.weather[0].description.slice(1) }}</h2>
    <p>{{ this.current.name }}</p>
    <h1>{{ Math.floor(this.current.main.temp) }}°C</h1>
    <div>
      <div>
      </div>
      <div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'BasicInfo',
  props: [
    'current',
    'conditionCodes',
    'night'
  ]
}
</script>
