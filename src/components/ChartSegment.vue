<template>
  <div id='{{id}}_charts' v-on:mouseover="showChartControlBar=true" v-on:mouseout="showChartControlBar=false" class="chart-segment">
    <div id='{{id}}_charts_control_bar' v-show='showChartControlBar' class="control-bar">
      <button type="button" class="btn btn-info navbar-btn" v-on:click='openConfiguration'>Configuration</button>
      <button type="button" class="btn btn-info navbar-btn">Data</button>
    </div>
    <lcharts :options='options'></lcharts>
    </div>
</template>

<style scoped>
  .control-bar {
    float:none;
    text-align: left;
    margin-left: 10%;
  }
  .chart-segment {
    display: inline;
    float: left;
    margin:10px 10px 10px 10px;
  }
  .chart-segment:hover {
    box-shadow: 0 0 0 3px #00b3ee;
    transition: all 200ms ease-out;
  }
</style>

<script>
  import Lcharts from './Lcharts.vue'

  export default {
    props: ['options', 'theme','showConfig','currentConfig'],
    components:{
      'lcharts':Lcharts
    },
    data: function () {
      return {
        chart: null,
        showChartControlBar:false
      }
    },
    methods: {
      openConfiguration: function(){
        this.showConfig = true;
        this.currentConfig = this.options;
      }
    }
  }
</script>
