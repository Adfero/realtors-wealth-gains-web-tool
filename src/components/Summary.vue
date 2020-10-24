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

export default {
  name: "Summary",
  props: ['selected','data','finalNumber'],
  data() {
    return {
      header: h3
    }
  },
  components: {
    AnimatedNumber
  },
  mounted() {
    // console.log('what is our selected and data',this.selected,this.data)
  },
  methods: {
    formatToPrice(value) {
      var price = `$${value.toFixed(0)}`
      return price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
  }
};
</script>

<style lang="scss" scoped>
.final-number {
  font-weight: 800;
  font-size: 50px;
  font-family: BrandonGrotesqueWeb-Bold, 'Work Sans', sans-serif;
  text-transform: uppercase;
}
</style>
