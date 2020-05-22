<template>
  <div>
    <div class="flex">
      <div class="metric-details"></div>       

      <svg :width="chart.width" :height="chart.height">
        <g :transform="translate(this.chart.margin.left, this.chart.margin.top)">
          <rect
            :width="chart.width - chart.margin.left - chart.margin.right"
            :height="chart.height - chart.margin.top - chart.margin.bottom"
            fill="lightblue"
          ></rect>
          <path
            v-for="(indicator, index) in metric.indicators"
            :d="path(indicator)"
            :stroke="colors[index]"
            stroke-width="3.5"
          >
          </path>
        </g>
        <g v-for="tick in xAxis()" :transform="translate(0, chart.height)">
          <g :transform="translate(tick.xOffset, 0)">
            <line y2="6"></line>
            <text>{{ tick.value }}</text>
          </g>
        </g>
      </svg>
    </div>
  </div>
</template>

<script>
import * as d3 from 'd3'

export default {
  props: {
    metric: Object
  },
  data () {
    return {
      colors: ['#5b6d7a', '#695b7a', '#7a695b', '#6d7a5b'],
      chart: {
        width: 600,
        height: 400,
        margin: {
          top: 20,
          bottom: 20,
          left: 20,
          right: 20
        },
      },
    }
  },
  methods: {
    xRange() {
      const years = this.metric.indicators.map(i => i.data.map(d => d.year))
      return d3.extent([].concat.apply([], years))
    },
    yRange() {
      return [this.metric.minValue, this.metric.maxValue]
    },
    boundedWidth() {
      return (this.chart.width - this.chart.margin.left - this.chart.margin.right)
    },
    boundedHeight() {
      return (this.chart.height - this.chart.margin.top - this.chart.margin.bottom)
    },
    xScale(value) {
      const x = d3.scaleLinear(this.xRange(), [0, this.boundedWidth()])
      return (value === undefined ? x : x(value))
    },
    yScale(value) {
      const y = d3.scaleLinear(this.yRange(), [0, this.boundedHeight()])
      return (value === undefined ? y : y(value))
    },
    viewbox(width, height) {
      return `0 0 ${width} ${height}`
    },
    path(indicator) {
      const line = d3.line().x(
        d => this.xScale(d.year)
      ).y(
        d => this.yScale(d.value)
      )
      return line(indicator.data)
    },
    xAxis() {
      const range = this.xRange()
      const numTicks = range[1] - range[0]
      const ticks = this.xScale().ticks(numTicks)
      return ticks.map(value => ({value, xOffset: this.xScale(value)}))
    },
    axis(indicator) {
      //console.log(xScale.ticks())
      //console.log(d3.axisBottom(xScale))
      return d3.axisBottom(this.xScale())
    },
    translate(left, top) {
      return `translate(${left},${top})`

    },
  },
  mounted () {
    //console.log(this.yScale().ticks())
    //console.log(d3)
    //console.log(this.metric)
  }
}
</script>

<style scoped>
svg {
  background: lightyellow;
}

.flex {
  display: flex;
}

.metric-details {
  width: 50%;
  background: lightgray;
}
</style>
