<template>
  <Temperature name="Temperature coventer" />
</template>

<script>
import Temperature from './components/Temperature.vue'

export default {
  name: 'Temperature coventer',
  components: {
    Temperature
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
  /* margin-top: 60px; */
}
</style>
