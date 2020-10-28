<template>
  <svg
    class="barchart"
    :width="width + marginLeft / 2"
    :height="height + marginTop"
  >
    <g :transform="`translate(0,20)`">
      <g
        class="x-axis"
        fill="none"
        :transform="`translate(0, ${height})`"
        style="color: #888"
      >
        <path
          class="domain"
          :stroke="currentColor"
          :d="`M0.5,0V0.5H${width}.0V0`"
        ></path>
        <g
          class="tick"
          opacity="1"
          font-size="10"
          font-family="sans-serif"
          text-anchor="middle"
          v-for="(bar, index) in bars"
          :key="index"
          :transform="`translate(${bar.x + bar.width / 2}, 0)`"
        >
          <line :stroke="currentColor" y2="6"></line>
          <text :fill="currentColor" y="9" dy="0.71em">{{ bar.xLabel }}</text>
        </g>
      </g>
      <g class="bars" fill="none">
        <rect
          v-for="(bar, index) in bars"
          :fill="bar.year == selectedYear ? '#61BA45' : '#175985'"
          :key="index"
          :height="bar.height"
          :width="bar.width"
          :x="bar.x"
          :y="bar.y"
          :class="bar.year == selectedYear ? 'active' : ''"
        ></rect>
        <text
          :fill="bar.negative == 'true' ? negativeColor : currentColor"
          v-for="(bar, index) in bars"
          :key="index"
          :x="bar.x"
          :y="(bar.y - 5)"
          :class="'bar-label'"
          >{{ bar.formatted }}</text>
      </g>
    </g>
  </svg>
</template>
<script>
import { scaleLinear, scaleBand } from "d3-scale";

export default {
  name: "BarChart",
  // props: ['dataset','selected'],
  props: {
    height: { default: 200 },
    width: { default: 520 },
    dataSet: { default: [] },
    marginLeft: { default: 0 },
    marginTop: { default: 0 },
    marginBottom: { default: 0 },
    marginRight: { default: 0 },
    tickCount: { default: 5 },
    barPadding: { default: 0.3 },
    selectedYear: { default: '' },
  },
  data() {
    return {
      height: 200,
      width: 520,
      currentColor: '#175985',
      negativeColor: '#EB1C24'
    };
  },
  mounted(){
    this.$nextTick(function() {
      window.addEventListener('resize', this.getWindowWidth);
      this.getWindowWidth()
    })
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.getWindowWidth);
  },
  methods: {
    getWindowWidth(event) {
      if(document.documentElement.clientWidth < 450) {
        this.width = 300
      }
      else if(document.documentElement.clientWidth >= 450 && document.documentElement.clientWidth < 640) {
        this.width = 400
      } else {
        this.width = 520
      }
    },
    formatPrice(value) {
      if(value > 1000000 || value < -1000000) {
        var price = Math.round(value/1000000)
        price = `$${price}M`
      } else if(value > 1000 || value < -1000 ) {
        var price = Math.round(value/1000)
        price = `$${price}K`
      } else {
        var price = `$${value}`
      }
      return price
    }
  },
  computed: {
    yTicks() {
      return this.y.ticks(this.tickCount);
    },
    x() {
      return scaleBand()
        .range([0, this.width])
        .padding(this.barPadding)
        .domain(this.dataSet.map((e) => e[0]));
    },
    y() {
      let values = this.dataSet.map((e) => e[1]);
      return scaleLinear()
        .range([this.height, 0])
        .domain([0, Math.max(...values)]);
    },
    bars() {
      let bars = this.dataSet.map((d) => {
        if(d[1] < 0) {
          return {
            xLabel: d[0] + ' yrs.',
            year: d[0],
            x: this.x(d[0]),
            y: 185,
            width: this.x.bandwidth(),
            height: this.height - this.y(d[1]), // TODO: look in to using TWEEN to animate this
            formatted: this.formatPrice(d[1]),
            negative: 'true'
          };
        } else if (d[1] == 0) {
          return {
            xLabel: d[0] + ' yrs.',
            year: d[0],
            x: this.x(d[0]) + 25,
            y: this.y(d[1]) - 10,
            width: this.x.bandwidth(),
            height: this.height - this.y(d[1]), // TODO: look in to using TWEEN to animate this
            formatted: '?',
            negative: 'false'
          };
        } else {
          return {
            xLabel: d[0] + ' yrs.',
            year: d[0],
            x: this.x(d[0]),
            y: this.y(d[1]),
            width: this.x.bandwidth(),
            height: this.height - this.y(d[1]), // TODO: look in to using TWEEN to animate this
            formatted: this.formatPrice(d[1]),
            negative: 'false'
          };
        }

      });

      return bars;
    },
  }
};
</script>

<style lang="scss" scoped>
@import '../variables.scss';
.barchart {
  .bar-label {
    font-size: 1.4rem;
    font-family: $font_brandon;
    @media all and (min-width: $screen-sm) {
      font-size: 2rem;
    }
  }
}
</style>
