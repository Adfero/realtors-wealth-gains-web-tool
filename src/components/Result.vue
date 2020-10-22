<template>
  <div class="result-container">
    <h2>For How Many Years?</h2>
    <div class="col-sm-12 select-year">
      <a class="clickable button col-sm-3" :class="{ 'active': selectedYear == '5' }" @click="revealData($event)" :data-value="data.five_year">5</a>
      <a class="clickable button col-sm-3" :class="{ 'active': selectedYear == '10' }" @click="revealData($event)" :data-value="data.ten_year">10</a>
      <a class="clickable button col-sm-3" :class="{ 'active': selectedYear == '15' }" @click="revealData($event)" :data-value="data.fifteen_year">15</a>
      <a class="clickable button col-sm-3" :class="{ 'active': selectedYear == '30' }" @click="revealData($event)" :data-value="data.thirty_year">30</a>
    </div>
    <div class="result-display" v-if="selectedYear && wealthGain">
      <div class="chart">
        <BarChart class="chart" :data="data" :selected="selectedYear" />
      </div>
      <div class="summary">
        <Summary :data="data" :selected="selectedYear"></Summary>
      </div>
    </div>
  </div>
</template>

<script>
import BarChart from './BarChart'
import Summary from './Summary'

export default {
  name: 'result',
  props: ['data'],
  data() {
    return {
      selectedYear: '',
      wealthGain: ''
    }
  },
  components: {
    BarChart, Summary
  },
  methods: {
    revealData(event){
      if(event.target.getAttribute('data-value') != '0'){
        console.log('we got into revealData, whats event',event.target)
        var elems = document.querySelectorAll("#app .result-container .select-year a")
        this.wealthGain = event.target.getAttribute('data-value')
        this.selectedYear = event.target.text
        console.log('wahoo',this.wealthGain,this.selectedYear)
      }

    }
  }
}
</script>
