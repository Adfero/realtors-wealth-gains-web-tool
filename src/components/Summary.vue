<template>
  <div class="summary col-sm-12 mb-4">
    <h3 class="uppercase mh-3">Your Results are In!</h3>
    <p class="w-80 margin-center" v-if="finalNumber > 0">Based on historical data from American homeowners, if you bought a home {{ selected }} years ago in the {{ data.metro }} area, the wealth gains from home price appreciation could be valued at</p>
    <p class="w-80 margin-center" v-else>Based on historical data from American homeowners, if you bought a home {{ selected }} years ago in the {{ data.metro }} area, the wealth gains from home price appreciation could be valued at</p>
    <div class="final-number animated">
      <animated-number
        :class="finalNumber < 0 ? 'red-txt' : 'blue-txt'"
        :value="finalNumber"
        :formatValue="formatToPrice"
        :duration="300"
        />
    </div>
    <p v-if="finalNumber < 0">...but be patient. It is normal for housing prices to fluctuate based on the market, but wealth gains always trend upwards over time. Keep an eye on housing prices in your area and consider holding on until prices rise again. Estimated gains may not be available for some years due to changes in metropolitan area delineations over time.</p>
  </div>
</template>
<script>
import AnimatedNumber from "animated-number-vue";

export default {
  name: "Summary",
  props: ['selected','data','finalNumber'],
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
