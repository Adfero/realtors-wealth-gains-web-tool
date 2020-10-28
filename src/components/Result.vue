<template>
  <div class="result-container text-align-center w-80 margin-center mb-6">
    <h2>For How Many Years?</h2>
    <div class="display-flex select-year">
      <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '5' }" @click="revealData($event)" :data-value="data.five_year">5</a>
      <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '10' }" @click="revealData($event)" :data-value="data.ten_year">10</a>
      <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '15' }" @click="revealData($event)" :data-value="data.fifteen_year">15</a>
      <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '30' }" @click="revealData($event)" :data-value="data.thirty_year">30</a>
    </div>
    <div class="money-background" v-if="selectedYear && wealthGain">
      <div class="result-display">
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

        <div class="share-restart row mt-4 text-align-center">
          <!-- <a class="btn-blue btn" href="/realtors-wealth-gains-web-tool/">Share</a> -->
          <a class="btn-blue btn" href="/realtors-wealth-gains-web-tool/">Start Over</a>
        </div>
      </div>
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
        // console.log('we got into revealData, whats event',event.target)
        var elems = document.querySelectorAll("#app .result-container .select-year a")
        this.wealthGain = event.target.getAttribute('data-value')
        this.selectedYear = event.target.text
        var propertyName = yearText[this.selectedYear]
        propertyName = propertyName + '_year'
        this.finalNumber = this.data[propertyName]
        this.dataFormatted.push(["5",this.data.five_year],["10",this.data.ten_year],["15",this.data.fifteen_year],["30",this.data.thirty_year])
      }

    }
  }
}
</script>

<style lang="scss" scoped>
@import '../variables.scss';
@import '../utils.scss';

.chart {
  margin: 120px auto;
  display: block;
}
#app .result-container {
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
      line-height: 1.6;
      flex: 0 0 70px;
      &[data-value="0"] {
        background: $color_gray !important;
        cursor: default;
      }
      &.active {
        background: $color_green !important;
      }
    }
  }
  .money-background {
    // background: url('/wp-content/plugins/realtors-wealth-gains-data-viz/js/realtors-wealth-gains/static/assets/cashfetti-long.svg');
    background: url('/wp-content/plugins/realtors-wealth-gains-data-viz/assets/cashfetti-long.svg');
    animation: animatedBackground 16s linear infinite;
    background-position: 0px 0px;
	  background-repeat: repeat;
  }
}
</style>
