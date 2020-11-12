<template>
  <div class="intro-container text-align-center">
    <div class="intro-content mb-6 w-80 margin-center">
      <h2>Building Wealth Through Homeownership</h2>
      <p>Homeownership is one of the best ways you can build wealth for yourself and future generations. Over time, your home’s value can appreciate which increases your personal wealth.</p>
      <p>Like any investment, wealth accumulation takes time. Follow the prompts to see how much your home’s value would likely have gained if you purchased a home in different areas in the U.S. 5, 10, 20, or 30 years ago.</p>
      <a class="intro-next btn-blue btn mt-2 padding-1 font-larger" @click="$emit('close')">Start Your Wealth Building</a>
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
@import '../variables.scss';
@import '../utils.scss';
.intro-next {
  height: 40px;
  font-size: 24px !important;
  @media all and (max-width: $screen-md) {
    font-size: 18px !important;
    height: auto !important;
    max-width: 100%;
    white-space: normal;
    line-height: 1.7;
  }
}
</style>
