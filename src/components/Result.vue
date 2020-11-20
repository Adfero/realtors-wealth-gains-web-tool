<template>
  <div class="result-container position-relative text-align-center">
    <div class="inner-container w-80 margin-center">
      <h2>For How Many Years?</h2>
      <div class="display-flex select-year">
        <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '5' }" @click="revealData($event)" :data-value="data.five_year">5</a>
        <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '10' }" @click="revealData($event)" :data-value="data.ten_year">10</a>
        <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '15' }" @click="revealData($event)" :data-value="data.fifteen_year">15</a>
        <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '30' }" @click="revealData($event)" :data-value="data.thirty_year">30</a>
      </div>

      <div class="result-display" id="results">
        <div class="money-background" v-if="selectedYear && wealthGain">
          <Summary :data="data" :selected="selectedYear" :finalNumber="finalNumber"></Summary>
          <div class="chart-wrapper mh-2">
            <BarChart
               class="chart"
               :dataSet="dataFormatted"
               :selectedYear="selectedYear"
               :margin-left="40"
               :margin-top="40"
               :tick-count="5"
               :bar-padding="0.5"
             />
          </div>

          <SummaryExtended :selected="selectedYear"></SummaryExtended>

          <div class="share-restart row text-align-center">
            <a class="btn-blue btn mt-2 start-over-btn" v-smooth-scroll @click="$emit('restart')">Start Over</a>
          </div>
        </div>
      </div>
    </div>
    <div class="illustration houses mt-5" v-if="selectedYear && wealthGain">
      <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/assets/NAR_HSA_WealthGains_Webtool_Illos_v1-01.svg" />
    </div>
    <div class="illustration realtor" v-if="selectedYear == '' && wealthGain == ''">
      <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/assets/realtor-character.svg" />
    </div>
  </div>
</template>

<script>
import BarChart from './BarChart'
import Summary from './Summary'
import SummaryExtended from './SummaryExtended'

var yearText = {
  '5': "five",
  '10': "ten",
  '15': "fifteen",
  '30': "thirty",
}

export default {
  name: 'result',
  props: ['data'],
  data() {
    return {
      selectedYear: '',
      wealthGain: '',
      finalNumber: '',
      dataFormatted: [],
    }
  },
  components: {
    BarChart, Summary, SummaryExtended
  },
  methods: {
    revealData(event){
      if(event.target.getAttribute('data-value') != '0'){
        var elems = document.querySelectorAll("#app .result-container .select-year a")
        this.wealthGain = event.target.getAttribute('data-value')
        this.selectedYear = event.target.text
        var propertyName = yearText[this.selectedYear]
        propertyName = propertyName + '_year'
        this.finalNumber = this.data[propertyName]
        this.dataFormatted.push(["5",this.data.five_year],["10",this.data.ten_year],["15",this.data.fifteen_year],["30",this.data.thirty_year])
        this.smoothScrollTo('#results')
      }
    },
    smoothScrollTo(hash){
      var $ = jQuery
      if (hash !== "") {
       $('html, body').animate({
         scrollTop: $(hash).offset().top - 40
       }, 400);
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../variables.scss';
@import '../utils.scss';

.chart {
  margin: 120px auto 60px;
  display: block;
}
#app .result-container {
  min-height: 600px;
  position: relative;
  @media all and (min-width: $screen-sm) {
    min-height: 500px;
  }
  .select-year {
    max-width: 100%;
    @media all and (min-width: $screen-sm) {
      max-width: 350px;
    }

    margin: 0 auto;
    align-items: center;
    justify-content: space-around;
    .button, .btn {
      width: 70px;
      height: 70px;
      font-size: 40px;
      text-align: center;
      flex: 0 0 70px;
      margin: 0 2px;
      display: flex;
      justify-content: center;
      align-content: center;
      padding: 0;
      flex-direction: column;
      &[data-value="0"] {
        background: $color_gray !important;
        cursor: default;
      }
      &.active {
        background: $color_green !important;
        @media all and (min-width: $screen-sm) {
          &:hover, &:focus {
            background: $color_dark_green !important;
          }
        }
      }
    }
  }
  .money-background {
    background: url('/wp-content/plugins/realtors-wealth-gains-data-viz/assets/cashfetti-long.svg');
    animation: animatedBackground 16s linear infinite;
    background-position: 0px 0px;
	  background-repeat: repeat;
    background-size: cover;
  }
  .start-over-btn {
    // height: 36px;
    height: auto;
  }
}
</style>
