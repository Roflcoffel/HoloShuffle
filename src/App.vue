<template>
  <h1>HoloShuffle</h1>
  <h4>Webapp for finding when hololive members sing eachothers songs.</h4>

  <div class="pure-g">
    <div class="pure-u-2-24"></div>
    <div class="pure-u-9-24">
      <Grid heading="Singer" side="left"/>
    </div>
    <div class="pure-u-2-24"></div>
    <div class="pure-u-9-24">
      <Grid heading="Original By" side="right"/>
    </div>
    <div class="pure-u-2-24"></div>
  </div>

  <Footer />
</template>

<script>
import Grid from './components/Grid.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Grid, Footer
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
