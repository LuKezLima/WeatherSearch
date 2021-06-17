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
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700;900&display=swap');
#app {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}
</style>
