<template>
  <h1>HoloShuffle</h1>
  <h4>Webapp for finding when hololive members sing eachothers songs.</h4>

  <div class="pure-g">
    <div class="pure-u-1-24"></div>
    <div class="pure-u-10-24"><Grid heading="Singer" /></div>
    <div class="pure-u-2-24"></div>
    <div class="pure-u-10-24"><Grid heading="Original By"/></div>
    <div class="pure-u-1-24"></div>
  </div>

  <div class="pure-g">
    <div class="pure-u-1-3"></div>
    <div class="pure-u-1-3"><p>here is some filler footer text.</p></div>
    <div class="pure-u-1-3"></div>
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
  color: #49c8f0;
  margin-top: 60px;
}
</style>
