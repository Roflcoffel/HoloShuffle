<template>
  <div class="pure-g">
    
  </div>
</template>

<script>
import holomen from '../db/holomen.json'

export default {
  name: 'GridComponent',
  data() {
    return {
      member: holomen
    }
  },
  props: {
    msg: String
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
