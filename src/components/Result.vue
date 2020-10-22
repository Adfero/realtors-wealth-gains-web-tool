<template>
  <div class="result-container">
    <h3>For How Many Years?</h3>
    <div class="col-sm-12">
      <a class="clickable button col-sm-3" :data-value="data.five_year">5</a>
      <a class="clickable button col-sm-3" :data-value="data.ten_year">10</a>
      <a class="clickable button col-sm-3" :data-value="data.fifteen_year">15</a>
      <a class="clickable button col-sm-3" :data-value="data.thirty_year">30</a>
    </div>
    <div class="chart">
      <BarChart class="chart" />
    </div>
    <div class="summary">

    </div>
  </div>
</template>

<script>
import BarChart from './BarChart'

export default {
  name: 'result',
  props: ['data'],
  components: {
    BarChart
  }
}
</script>
