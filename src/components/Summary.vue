<template>
  <div class="summary">
    <h3 class="uppercase">{{ header[selected] }}!</h3>
    <p>After owning your home for {{ selected }} years in the {{ data.metro }} area, your house would have appreciated by about</p>
    <div class="navy-text final-number animated">
      <animated-number
        :value="finalNumber"
        :formatValue="formatToPrice"
        :duration="300"
        />
    </div>
    <a class="btn-blue btn" href="/realtors-wealth-gains-web-tool/">Start Over</a>
  </div>
</template>
<script>
import AnimatedNumber from "animated-number-vue";

var h3 = {
  '5': 'Nice!',
  '10': 'Yes!',
  '15': 'Wow!',
  '30': 'Whoa!',
};
var bodyCopy = {
  '5': 'Nice!',
  '10': 'Yes!',
  '15': 'Wow!',
  '30': 'Whoa!',
};
export default {
  name: "Summary",
  props: ['selected','data','finalNumber'],
  data() {
    return {
      header: h3,
      body: bodyCopy
    }
  },
  components: {
    AnimatedNumber
  },
  mounted() {
    console.log('what is our selected and data',this.selected,this.data)
  },
  methods: {
    formatToPrice(value) {
      return `$${value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",").toFixed(0)}`;
    }
  }
};
</script>

<style lang="scss">
</style>
