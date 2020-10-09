<template>
  <div class="container">
    <intro v-if="introLoad" @close="goToLocation()"></intro>
    <locationPrompt v-if="location"></locationPrompt>
  </div>
</template>

<script>
import Intro from './Intro'
import LocationPrompt from './LocationPrompt'

export default {
  name: 'WebTool',
  data () {
    return {
      isMobile: false,
      introLoad: true,
      prompted: true,
      location: false,
      years: false
    }
  },
  components: {
    Intro, LocationPrompt
  },
  mounted() {
    // load intro
    if(this.introLoad){
      this.introLoad = true
    }
  },
  methods: {
    goToLocation() {
      this.introLoad = false
      this.location = true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
  span {
    color: red;
  }
}
</style>
