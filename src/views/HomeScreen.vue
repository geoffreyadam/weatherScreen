<template>
  <div>
    <MainInfo :current="current" :conditionCodes="conditionCodes" :night="night"></MainInfo>
    <SideBar :current="current"></SideBar>
    <BackgroundImage v-if="current" :current="current" :conditionCodes="conditionCodes"></BackgroundImage>
  </div>
</template>
<script>
import axios from 'axios'
import BackgroundImage from '../components/BackgroundImage'
import MainInfo from '../components/MainInfo'
import SideBar from '../components/SideBar'
import conditionCodes from '../assets/conditionCodes'
export default {
  name: 'HomeScreen',
  components: {
    SideBar,
    MainInfo,
    BackgroundImage
  },
  data () {
    return {
      current: this.current,
      night: this.night,
      forecast: this.forecast,
      conditionCodes: conditionCodes
    }
  },
  methods: {
    isItNight () {
      const now = Date.now()
      if (this.sunriseStamp > now || this.sunsetStamp < now) {
        this.night = true
      } else {
        this.night = false
      }
    },
    fetchApi () {
      axios.get('https://api.openweathermap.org/data/2.5/forecast?q=Bordeaux&units=metric&lang=fr&cnt=24&appid=' + process.env.VUE_APP_FORECAST_KEY)
        .then((response) => {
          if (response.status === 200) {
            this.putForecastInArray(response.data.list)
          }
        })
      axios.get('https://api.openweathermap.org/data/2.5/weather?units=metric&lang=fr&q=Bordeaux&appid=' + process.env.VUE_APP_WEATHER_KEY)
        .then((response) => {
          if (response.status === 200) {
            this.current = response.data
            this.isItNight()
            console.log(this.current)
          }
        })
    },
    startInterval () {
      setInterval(() => {
        this.fetchApi()
      }, 50000)
    },
    putForecastInArray (data) {
      const forecast = []
      // if (this.forecast.length > 0) {
      //   forecast = this.forecast
      // }
      data.forEach((oneHourWeather) => {
        forecast.splice(oneHourWeather.dt, 0, oneHourWeather)
      })
      this.forecast = data
    }
  },
  mounted () {
    this.fetchApi()
    this.startInterval()
  }
}
</script>
