<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search..." @keypress="fetchWeather" v-model="query"/>
      </div>

      

      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">Los Angeles</div>
          <div class="date">Friday 9th Oct 2020</div>
        </div>

        <div class="weather-box">
          <div class="temp">70 deg</div>
          <div class="weather">Sunny</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) { 
      if(e.key == "Enter"){
        fetch(`${process.env.VUE_APP_URL}weather?q=${this.query}&units=metric&APPID=${process.env.VUE_APP_API}`)
        .then(res => {
          return res.json()
        })
        .then(this.setResults)
      }
    },
    setResults(result){
      this.weather = result
      console.log(this.weather)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
