<template>
  <div id="app">
    <div id="metrics">
      <div id="totalScore">
        {{ totalScore }}
      </div>
      <div class="flex">
        <MetricBox
          v-for="metric in metrics"
          @select-metric="selectMetric(metric)"
          :metric="metric"
          :key="metric.name"
        />
      </div>
      <transition name="fade">
        <div id="metricPane" v-if="selectedMetric !== undefined">
          Dimension:
          <IndicatorChart :metric="selectedMetric"/>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import MetricBox from '@/components/MetricBox'
import IndicatorChart from '@/components/IndicatorChart'

export default {
  name: 'App',
  components: {
    MetricBox, IndicatorChart
  },
  methods: {
    selectMetric(metric) {
      this.selectedMetric = (this.selectedMetric === metric ? undefined : metric)
    }
  },
  data () {
    return {
      totalScore: 80,
      selectedMetric: undefined,
      metrics: [
        {
          'name': 'Life Expectancy',
          'indexScore': 58.5,
          'slope': 0.1,
          'indicators': [
            {
              'name': 'Health-Adjusted Life Expectancy'
            }
          ]
        },
        {
          'name': 'Median Household Income',
          'indexScore': 76.0,
          'slope': -0.2
        },
        {
          'name': 'Mental Health',
          'indexScore': 58.5,
          'slope': 0.1,
          'minValue': 0,
          'maxValue': 100,
          'indicators': [
            {
              'name': 'Any Mental Illness',
              'description': 'Percentage of adults with any mental illness',
              'data': [
                {
                  'year': 1988,
                  'value': 30.9
                },
                {
                  'year': 1989,
                  'value': 31.0
                },
                {
                  'year': 1990,
                  'value': 32.4
                },
                {
                  'year': 1991,
                  'value': 33.5
                },
              ]
            },
            {
              'name': 'Serious Mental Illness',
              'description': 'Percentage of adults with at least one serious mental illness',
              'data': [
                {
                  'year': 1990,
                  'value': 12.4
                },
                {
                  'year': 1991,
                  'value': 13.2
                },
              ]
            }
          ]
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

.fade-enter-active {
  transition: opacity 0.25s ease-out;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
