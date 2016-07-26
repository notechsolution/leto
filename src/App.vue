<template>
  <div id="app" >
    <img class="logo" src="./assets/logo.png">
    <hello></hello>
    <p>
      Welcome to your Vue.js app!
    </p>
  </div>
  <div id="charts">
    <lcharts :options='polar'></lcharts>
    <lcharts :options='bar' v-ref:bar></lcharts>
  </div>
</template>

<script>
import Hello from './components/Hello'
import Lcharts from './components/Lcharts.vue'
import echarts from 'echarts'

let asyncData = {
  categories: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"],
  data: [5, 20, 36, 10, 10, 20]
}

export default {
  components: {
    Hello,
    Lcharts
  },
  data: function () {
    let data = []
    for (let i = 0; i <= 360; i++) {
      let t = i / 180 * Math.PI;
      let r = Math.sin(2 * t) * Math.cos(2 * t);
      data.push([r, i]);
    }
    return {
      polar: {
        title: {
          text: '极坐标双数值轴'
        },
        legend: {
          data: ['line']
        },
        polar: {
          center: ['50%', '54%']
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          }
        },
        angleAxis: {
          type: 'value',
          startAngle: 0
        },
        radiusAxis: {
          min: 0
        },
        series: [
          {
            coordinateSystem: 'polar',
            name: 'line',
            type: 'line',
            showSymbol: false,
            data: data
          }
        ],
        animationDuration: 2000
      },
      bar: {
        title: {
          text: '异步数据加载示例'
        },
        tooltip: {},
        legend: {
          data:['销量']
        },
        xAxis: {
          data: []
        },
        yAxis: {},
        series: [{
          name: '销量',
          type: 'bar',
          data: []
        }]
      }
    }
  },
  ready: function(){
// simulating async data from server
    setTimeout(() => {
      this.$refs.bar.mergeOptions({
      xAxis: {
        data: asyncData.categories
      },
      series: [{
        name: '销量',
        data: asyncData.data
      }]
    })
  }, 3000)
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#charts {
  color: #2c3e50;
  margin-top: 200px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
