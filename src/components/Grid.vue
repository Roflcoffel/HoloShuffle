<template>
  <h2>{{heading}}</h2>
  <div class="pure-g" v-for="i in 8" :key="i">
    <div class="pure-u-1-5" v-for="(file, memberKey) in icons[i-1]" :key="memberKey">
      <div v-if="side === 'left' && i === 8"></div>
      <div v-else>
        <img :id="addName(memberKey, side)" :class="addGreyscale(memberKey, side)" :src="`./assets/${file}`"
          @mouseenter="addHighlight($event, memberKey, side)"
          @mouseleave="addHighlight($event, memberKey, side)"
          @click="onSelection($event, memberKey, side)"
        />
      </div>
    </div>
    <div class="pure-u-1-1" v-for="(file, memberKey) in icons[i-1]" :key="memberKey">
      <SongList v-if="side === 'right'" :id="addName(memberKey, side)"  class="hide" :songs="selCovered" />
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
      console.log("Unlocking: " + this.member)
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
    console.log("Locking: " + this.member + " " + this.isLocked)
  }
}

let leftLockedElement = new LockedElement()
let rightLockedElement = new LockedElement()

export default {
  name: 'Grid_Component',
  components: {
    SongList
  },
  data() {
    return {
      icons: icons_file,
      covered: covered_file,
      leftLock: leftLockedElement,
      rightLock: rightLockedElement,
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
    addHighlight(event, member, side) {
      if(side == "left") {
        //Turn of hover and greyscale when an element is locked.
        if(this.leftLock.isLocked) return
        event.target.classList.toggle("hover")

        for(let stream of this.covered[member]) {
          let img = document.querySelector("img#" + stream.by)
          img.classList.toggle("greyscale")
        }
      }
      else {
        if(this.rightLock.isLocked) return
        event.target.classList.toggle("hover")
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
            this.toggleSongList("div#" + member)
          },
          () => {
            this.toggleSongList("div#" + member)
          }
        )
        return
      }

      if(side == "left") {
        this.leftLock.lock(
          member,
          () => event.target.classList.add("hover"),
          () => console.log("Empty Unlock Function")
        )
      }
    },

    toggleSongList(query) {
      const elem = document.querySelector(query)
      elem.classList.toggle("show")
      elem.classList.toggle("hide")
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
  height: 115px;
  box-shadow: 2px 2px 5px black;
  position: relative;
  margin-top: 5px;
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
