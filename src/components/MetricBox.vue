<template>
  <div @click="$emit('select-metric')" id="metricContainer">
    <div id="metricBox" :class="slopeType(metric.slope)">
      {{ metric.indexScore }}
    </div>
    <div id="metricName">
      {{ metric.name }}
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      metric: Object
    },
    methods: {
      slopeType: (slope) => {
        if (slope > 0) {
          return 'increasing'
        } else if (slope < 0) {
          return 'decreasing'
        } else {
          return 'constant'
        }
      }
    }
  }
</script>

<style scoped>
#metricContainer {
  width: 10em;
  border: 1px solid black;
  margin: 0.5em;
  background: #5fa6c6;
}

#metricContainer:hover {
  cursor: pointer;
}

#metricBox {
  display: flex;
  height: 5em;
  justify-content: center;
  align-items: center;
  font-size: xx-large;
  border-bottom: 1px solid black;
  color: white;
}

#metricName {
  color: white;
  text-align: center;
  padding-top: 0.2em;
  padding-bottom: 0.2em;
}

.increasing {
  background: green;
}

.decreasing {
  background: red;
}

.constant {
  background: lightgrey;
}
</style>
