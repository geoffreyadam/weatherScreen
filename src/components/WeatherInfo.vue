<template>
    <article>
      <i class="wi" :class="this.icon"></i>
      <div>
        <h3>{{ this.title }}</h3>
        <p>{{ Math.floor(this.value) }} {{ this.unit }}</p>
      </div>
    </article>
</template>
<script>
export default {
  name: 'WeatherInfo',
  props: [
    'icon',
    'title',
    'value',
    'unit'
  ]
}
</script>
