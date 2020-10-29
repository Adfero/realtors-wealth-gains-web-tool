<template>
  <div class="intro-container text-align-center mb-3">
    <div class="intro-content mb-5 w-80 margin-center">
      <h2>Building Wealth Through Homeownership</h2>
      <p>Owning a home is one of the best ways you can build wealth for yourself and future generations. Follow the prompts to see how much wealth you can build by purchasing a home in different areas in the U.S.</p>
      <a class="intro-next btn-blue btn mt-2" @click="$emit('close')">Next</a>
    </div>
    <div class="illustration mt-5 houses">
      <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/assets/NAR_HSA_WealthGains_Webtool_Illos_v1-01.svg" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'intro'
}
</script>
<style lang="scss" scoped>
.intro-next {
  height: 36px;
}
</style>
