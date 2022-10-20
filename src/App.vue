<template>
  <div id="app">
    <PriceCalendar msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import PriceCalendar from './components/PriceCalendar.vue'

export default {
  name: 'App',
  components: {
    PriceCalendar
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
