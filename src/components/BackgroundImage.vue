<template>
  <div>
    <img v-if="this.backgroundImage" class="back-img" :src="backgroundImage" alt="">
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'BackgroundImage',
  data () {
    return {
      tag: this.tag,
      backgroundImage: this.backgroundImage
    }
  },
  props: [
    'current',
    'conditionCodes'
  ],
  methods: {
    setBackgroundImage () {
      if (this.tag !== this.conditionCodes[this.current.weather[0].id].tag) {
        this.tag = this.conditionCodes[this.current.weather[0].id].tag
        axios.get('https://api.unsplash.com/photos/random?client_id=' . process.env.VUE_APP_UNSPLASH_KEY . '&orientation+landscape&query=' + this.conditionCodes[this.current.weather[0].id].tag)
          .then((response) => {
            this.backgroundImage = response.data.urls.full
          })
      }
    }
  },
  watch: {
    current: function () {
      this.setBackgroundImage()
    }
  },
  mounted () {
    this.setBackgroundImage()
  }
}
</script>
