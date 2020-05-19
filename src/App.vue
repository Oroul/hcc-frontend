<template>
  <div id="app">
    <div id="metrics">
      <div id="totalScore">
        {{ totalScore }}
      </div>
      <div v-if="selectedMetric === undefined" class="flex">
        <MetricBox
          v-for="metric in metrics"
          @select-metric="selectMetric(metric)"
          :metric="metric"
          :key="metric.name"
        />
      </div>
      <div v-else>
        <div id="metricPane">
          <MetricBox
            :metric="selectedMetric"
            @select-metric="selectMetric(selectedMetric)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MetricBox from '@/components/MetricBox'

export default {
  name: 'App',
  components: {
    MetricBox
  },
  methods: {
    selectMetric(metric) {
      console.log('selectMetric')
      this.selectedMetric = (this.selectedMetric === undefined ? metric : undefined)
    }
  },
  data () {
    return {
      totalScore: 80,
      selectedMetric: undefined,
      metrics: [
        {
          'name': 'Health-Adjusted Life Expectancy',
          'indexScore': 58.5,
          'slope': 0.1
        },
        {
          'name': 'Median Household Income',
          'indexScore': 76.0,
          'slope': -0.2
        },
        {
          'name': 'Mental Health',
          'indexScore': 58.5,
          'slope': 0.1
        },
        {
          'name': 'Childhood Success Rate',
          'indexScore': 46.0,
          'slope': 0
        },
        {
          'name': 'Social and Economic Mobility',
          'indexScore': 88.5,
          'slope': 0.1
        },
        {
          'name': 'Absence of Substance Abuse',
          'indexScore': 36.0,
          'slope': -0.2
        },
        {
          'name': 'Metric #7',
          'indexScore': 53.3,
          'slope': 0.1
        },
        {
          'name': 'Metric #8',
          'indexScore': 76.0,
          'slope': -0.2
        }
      ]
    }
  }
}
</script>

<style>
#metrics {
  border: 1px dotted black;
  margin-left: 10%;
  margin-right: 10%;
}

#totalScore {
  text-align: center;
  font-size: xxx-large;
  border: 1px dotted black;
}

#metricPane {
  border: 1px dotted black;
}

.flex {
  display: flex;
}
</style>
