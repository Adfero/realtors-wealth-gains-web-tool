<template>
  <div class="intro-container text-align-center mb-5">
    <div class="intro-content mb-5">
      <h2>Building Wealth Through Homeownership</h2>
      <p>Owning a home is one of the best ways you can build wealth for yourself and future generations. Follow the prompts to see how much wealth you can build by purchasing a home in different areas in the U.S.</p>
      <a class="intro-next btn-blue btn" @click="$emit('close')">Next</a>
    </div>
    <div class="illustration mt-5">
      <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/js/realtors-wealth-gains/static/assets/NAR_HSA_WealthGains_Webtool_Illos_v1-01.svg" />
      <!-- TODO: uncomment this when ready to deploy <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/assets/NAR_HSA_WealthGains_Webtool_Illos_v1-01.svg" /> -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'intro'
}
</script>
