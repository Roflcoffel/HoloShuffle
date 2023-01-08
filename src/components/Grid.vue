<template>
  <h2>{{heading}}</h2>
  <div class="pure-g" v-for="i in 8" :key="i">
    <div class="pure-u-1-5" v-for="(file, memberKey) in icons[i-1]" :key="memberKey">
      <div v-if="side === 'left' && i === 8"></div>
      <div v-else>
        <img :id="addName(memberKey, side)" :class="addGreyscale(memberKey, side)" :src="`./assets/${file}`"
          @mouseenter="addHighlight(memberKey, side)"
          @mouseleave="addHighlight(memberKey, side)"
          @click="onSelection($event, memberKey, side)"
        />
        <SongList v-if="side === 'right'" :id="addName(memberKey, side)"  class="hide" :songs="selCovered" />
      </div>
    </div>
  </div>
</template>

<script>
import icons_file from '../db/icons.json'
import covered_file from '../db/covered.json'

import SongList from './SongList.vue'

class LockedElement {
  constructor() {
    this.member = ""
    this.isLocked = false
  }

  //sets a lock on a specific member.
  lock(member, onLock, onUnlock) {
    //Clicked on the same member again, unlock it.
    if(this.member == member) {
      onUnlock()
      this.member = ""
      this.isLocked = false
      return
    }

    //Clicked on any element while locked just return.
    if(this.isLocked) return

    //No active lock for this object, so lock it.
    this.member = member
    this.isLocked = true
    onLock()
  }
}

export default {
  name: 'Grid_Component',
  components: {
    SongList
  },
  data() {
    return {
      icons: icons_file,
      covered: covered_file,
      leftLock: new LockedElement(),
      rightLock: new LockedElement(),
      selCovered: []
    }
  },
  props: {
    heading: String,
    side: String,
  },
  methods: {
    addGreyscale(member, side) {
      if(side == "right") return "greyscale"
      if(this.covered[member] === undefined) return "greyscale"
    },
    addName(member, side) {
      if(side == "right") return member
    },
    addHighlight(member, side) {
      if(this.leftLocked) return
      if(side == "left") {
        for(let stream of this.covered[member]) {
          let img = document.getElementById(stream.by)
          img.classList.toggle("greyscale")
        }
      }
    },
    //Handle when selecting singer, and originalby.
    onSelection(event, member, side) {
      if(side == "right" && this.leftLock.isLocked) {
        this.rightLock.lock(
          member,
          () => {
            event.target.classList.add("hover")
            this.selCovered = this.getCoveredSongs(member)
            this.switchClass("SongList#" + member, "show", "hide")
          },
          () => {
            event.target.classList.remove("hover")
            this.switchClass("SongList#" + member, "hide", "show")
          }
        )
        return
      }
      
      this.leftLock.lock(
        member,
        () => event.target.classList.add("hover"),
        () => event.target.classList.remove("hover")
      )

      //the two ways we should be able to get out of the locked state is
      //1. click on the same member again
      //2. clicking a highlighted member on the right and then also selected a song

      //little about how this looks visually,
      //after selecting a member on the left, the rest of the member on the left side
      //greyed out, and the clicked member is now always zoomed in maybe even add an extra highlight to it.
      //you can then hover over on the right side, and when you click them a list under their portrait will appear
      //this are all the songs that are made by the selected member and also covered by the first selected member.
      //when then selecting a song in this list, a video will popout from under the portrait of the first selected member.
      
      //this should also unlock everything again, and the video disappears if we click on another member on the left side,
      //or we have a little close button in the upper top right of the video.
    },

    //removes one class and adds another.
    switchClass(element_id, remove_class, add_class) {
      const elem = document.getElementById(element_id)
      elem.classList.add(add_class)
      elem.classList.remove(remove_class)
    },

    //gets the covers that the currently locked member has sung from a specific member.
    getCoveredSongs(member) {
      return this.covered[this.leftLock.member].filter((stream) => stream.by == member)
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

.hover {
  z-index: 2;
  transform: scale(1.5);
}
.greyscale {
  z-index: -1;
  filter: grayscale(100%);
}

.hide {
  display: none;
}

.show {
  display: block;
}
</style>
