<template>
  <br/>
  <br/>
  <div class="pure-g">
      <div class="pure-u-1-3"></div>
      <div class="pure-u-1-3"><h3>Offical Shuffle Melody!</h3></div>
      <div class="pure-u-1-3"></div>
  </div>

  <div class="pure-g">
    <div class="pure-u-1-5"></div>
    <div class="pure-u-3-5">
        <iframe width="560" height="315" :src="shuffle_melody" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
    </div>
    <div class="pure-u-1-5"></div>
  </div>

  <br/>
  <br/>

  <div class="pure-g">
    <div class="pure-u-1-3"></div>
    <div class="pure-u-1-3">
      <p>The project can be found here <a :href="github_url">HoloShuffle@GitHub</a></p>
    </div>
    <div class="pure-u-1-3"></div>
  </div>
</template>

<script>
export default {
    name: "Footer_Component",
    data() {
        return  {
            github_url: "https://github.com/Roflcoffel/HoloShuffle",
            shuffle_melody: "https://www.youtube.com/embed/SirMcRmSEB4"
        }
    }
}
</script>

<style scoped>

</style>
