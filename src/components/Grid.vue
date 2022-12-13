<template>
  <h2>{{heading}}</h2>
  <div class="pure-g" v-for="i in 7" :key="i">
    <div class="pure-u-1-5" v-for="(file, key) in Icons[i-1]" :key="key">
      <img :src="`./assets/${file}`" />
    </div>
  </div>
</template>

<script>
import icons from '../db/icons.json'
import covered from '../db/covered.json'

export default {
  name: 'GridComponent',
  data() {
    return {
      Icons: icons,
      Covered: covered
    }
  },
  props: {
    heading: String
  }
}
</script>

<style scoped>
img {
  transition: transform .2s;
  width: auto;
  height: 130px;
  box-shadow: 2px 2px 5px black;
}  
img:hover {
  transform: scale(1.5);
}
</style>
