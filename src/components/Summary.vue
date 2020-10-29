<template>
  <div class="summary col-sm-12 mb-4">
    <h3 class="uppercase mh-3">{{ header[selected] }}</h3>
    <p class="w-80 margin-center">After owning your home for {{ selected }} years in the {{ data.metro }} area, your house would have appreciated by about</p>
    <div class="final-number animated">
      <animated-number
        :class="finalNumber < 0 ? 'red-txt' : 'blue-txt'"
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
  methods: {
    formatToPrice(value) {
      var price = `$${value.toFixed(0)}`
      return price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
  }
};
</script>

<style lang="scss" scoped>
@import '../variables.scss';
.final-number {
  font-weight: 800;
  font-size: 50px;
  font-family: $font_brandon_bold;
  text-transform: uppercase;
}
.summary {
  p {
    font-size: 24px;
  }
}
</style>
