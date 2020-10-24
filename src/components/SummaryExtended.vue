<template>
  <div class="summary-extended text-align-center">
    <div class="col-sm-6 text-align-left">
      <h3 class="uppercase">{{ header[selected] }}!</h3>
      <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/js/realtors-wealth-gains/static/assets/realtor-character.svg" />
    </div>
    <div class="col-sm-6 text-align-left">
      <p>{{ body[selected] }}</p>
    </div>
    <div class="share-restart">
      <a class="btn-blue btn" href="/realtors-wealth-gains-web-tool/">Share</a>
      <a class="btn-blue btn" href="/realtors-wealth-gains-web-tool/">Start Over</a>
    </div>
  </div>
</template>
<script>
var h3 = {
  '5': 'The Short Stay',
  '10': 'The Average Stay',
  '15': 'The Grade School Stay',
  '30': 'The Forever Home',
};

var bodyCopy = {
  '5': 'Owning a home for just 5 years is a great investment. Home prices increase each year, which means in 5 years you can sell your home for much more than you paid for it. You can use the wealth you’ve built to upgrade to a larger home, take your dream vacation or however you choose!',
  '10': 'If you’ve stayed in your home for 10 years, you’re in a good place to make a sizeable profit when you sell. If you’ve made improvements to your home during your stay, you will have built even more wealth!',
  '15': 'You build wealth when your home appreciates in value and you pay down the principal on your mortgage. After 15 years, you will have paid down a significant portion of your mortgage and your home will be worth a lot more than when you bought it! If you make improvements to your home during this time you can accumulate even more wealth!',
  '30': 'By this time you’ve paid off the principal on your mortgage and the total value of your home when you sell it or pass it on will be the wealth you’ve built. Your home will have substantially increased in value in 30 years, even more so if you’ve made improvements, so you can sell your home for much more than you paid and make a profit or pass along this asset to your family!',
};

var summaryImg = {

};

export default {
  name: "SummaryExtended",
  props: ['selected'],
  data() {
    return {
      header: h3,
      body: bodyCopy
    }
  }
};
</script>

<style lang="scss">
</style>
