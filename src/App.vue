<template>
  <div id="app">
    <WeatherApp> </WeatherApp>

  </div>
</template>

<script>
import WeatherApp from './components/WeatherApp.vue'


export default {
  name: 'App',
  components: {
    WeatherApp
  
    
  }
}
</script>

<style>
#app {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
