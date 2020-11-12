<template>
  <div class="summary-extended text-align-center row">
    <div class="col-sm-6 text-align-left">
      <h3 class="uppercase">{{ header[selected] }}</h3>
      <img class="w-100 padding-1 mb-2" :src="'/wp-content/plugins/realtors-wealth-gains-data-viz/assets/'+img[selected]" />
    </div>
    <div class="col-sm-6 text-align-left mt-6 body-copy">
      <p>{{ body[selected] }}</p>
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
  '5': 'Owning a home for just 5 years is a great investment. Home prices can increase each year, which means in 5 years you can sell your home for more than you paid for it. You can use the wealth you’ve accumulated to upgrade to a larger home, take your dream vacation or however you choose!',
  '10': 'If you have owned your home for 10 years, you are in a good place to make a sizeable profit when you sell. Making improvements to your home during can help you improve your wealth gains as well!',
  '15': 'You build wealth when your home appreciates in value and you pay down the principal on your mortgage. After 15 years, you will have paid down a significant portion of your mortgage and your home can be worth a lot more than when you bought it! If you make improvements to your home during this time you can accumulate even more wealth!',
  '30': 'After 30 years in your dream home, you’ve paid off the principal on your mortgage and may be ready to sell it or pass it down to the next generation of your value. Your home’s value could increase substantially after 30 years, even more so if you’ve made improvements, so you can sell your home for much more than you paid and make a profit or use this asset to help the next generation of your family build on this wealth!',
};

var summaryImg = {
  '5': 'short-stay.svg',
  '10': 'average-stay.svg',
  '15': 'grade-school-stay.svg',
  '30': 'forever-home.svg',
};

export default {
  name: "SummaryExtended",
  props: ['selected'],
  data() {
    return {
      header: h3,
      body: bodyCopy,
      img: summaryImg
    }
  }
};
</script>

<style lang="scss" scoped>
@import '../variables.scss';
@import '../utils.scss';
@media all and (max-width: $screen-md) {
  .body-copy {
    margin-top: 0 !important;
  }
}
</style>
