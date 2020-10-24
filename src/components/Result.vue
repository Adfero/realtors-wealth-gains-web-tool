<template>
  <div class="result-container text-align-center">
    <h2>For How Many Years?</h2>
    <div class="display-flex select-year">
      <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '5' }" @click="revealData($event)" :data-value="data.five_year">5</a>
      <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '10' }" @click="revealData($event)" :data-value="data.ten_year">10</a>
      <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '15' }" @click="revealData($event)" :data-value="data.fifteen_year">15</a>
      <a class="clickable btn-blue btn" :class="{ 'active': selectedYear == '30' }" @click="revealData($event)" :data-value="data.thirty_year">30</a>
    </div>
    <div class="result-display" v-if="selectedYear && wealthGain">
      <div class="summary">
        <Summary :data="data" :selected="selectedYear" :finalNumber="finalNumber"></Summary>
      </div>
      <div class="chart mh-2">
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
      <div class="summary">
        <SummaryExtended :selected="selectedYear"></SummaryExtended>
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
        this.dataFormatted.push(["5 yrs.",this.data.five_year],["10 yrs.",this.data.ten_year],["15 yrs.",this.data.fifteen_year],["30 yrs.",this.data.thirty_year])
      }

    }
  }
}
</script>

<style lang="scss" scoped>
@import '../variables.scss';
.chart {
  margin: 120px auto;
  display: block;
}
.result-container {
  .select-year {
    max-width: 30%;
    margin: 0 auto;
    align-items: center;
    justify-content: space-around;
    .button, .btn {
      width: 65px;
      height: 65px;
      font-size: 40px;
      &[data-value="0"] {
        background: $color_gray;
        cursor: default;
      }
      &.active {
        background: $color_green;
      }
    }
  }
}
</style>
