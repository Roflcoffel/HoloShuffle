<template>
  <h1>HoloShuffle</h1>
  <h4>Webapp for finding when hololive members sing eachothers songs.</h4>

  <div class="pure-g">
    <div class="pure-u-1-24"><p style="background-color: black; color:white">Empty</p></div>
    <div class="pure-u-10-24"><Grid msg="Wow"/></div>
    <div class="pure-u-2-24"><p style="background-color: black; color:white">Empty</p></div>
    <div class="pure-u-10-24"><Grid msg="Wow"/></div>
    <div class="pure-u-1-24"><p style="background-color: black; color:white">Empty</p></div>
  </div>
</template>

<script>
import Grid from './components/Grid.vue'

export default {
  name: 'App',
  components: {
    Grid
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
