<template>
  <h2>{{heading}}</h2>
  <div class="pure-g" v-for="i in 7" :key="i">
    <div class="pure-u-1-5" v-for="(file, key) in Icons[i-1]" :key="key">
      <img @mouseover.once="addHighlight($event, key, side)" :class="addGreyscale(key, side)" :src="`./assets/${file}`" />
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
    heading: String,
    side: String
  },
  methods: {
    addGreyscale(member, side) {
      if(side == "right") return "greyscale"
      if(this.Covered[member] === undefined) return "greyscale"
    },
    addHighlight(event, member, side) {
      if(side == "left") {
        console.log(event.target);
        //when hovering over a non undefined member
        //on the left side

        //highlight the person that is returned from the
        //covered data file.

        //to do it would be best if we could add the name as id
        //to each image, so we can just getby id and then remove the greyscale class

        //but when we leave this we need to readd the greyscale again.
      }
    }
  }
}
</script>

<style scoped>

img {
  z-index: 1;
  transition: transform .2s;
  width: auto;
  height: 130px;
  box-shadow: 2px 2px 5px black;
  position: relative;
}  
img:hover {
  z-index: 2;
  transform: scale(1.5);
}
.greyscale {
  z-index: -1;
  filter: grayscale(100%);
}
</style>
