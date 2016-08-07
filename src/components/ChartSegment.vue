<template>
  <div id='{{id}}_charts' v-on:mouseover="showChartControlBar=true" v-on:mouseout="showChartControlBar=false" class="chart-segment">
    <div id='{{id}}_charts_control_bar' v-show='showChartControlBar' class="control-bar">
      <button type="button" class="btn btn-default navbar-btn no-border" v-on:click='openConfiguration'>
        <span class="glyphicon glyphicon-cog" aria-hidden="true"></span>
      </button>
      <button type="button" class="btn btn-default navbar-btn no-border">
        <span class="glyphicon glyphicon-list" aria-hidden="true"></span>
      </button>
      <button type="button" class="btn btn-default navbar-btn no-border" @click='showDeletionConfirmModal = true'>
        <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
      </button>
    </div>
    <div v-show='showChartControlBar==false' style="height:48px"></div>
    <lcharts :options='options'></lcharts>
    </div>

  <modal :show.sync="showDeletionConfirmModal" effect="fade">
    <div slot="modal-header" class="modal-header">
      <h4 class="modal-title">
         Delete Confirmation
      </h4>
    </div>
    <div slot="modal-body" class="modal-body">Do you want to <b>DELETE</b> the chart? It cannot Undo</div>
    <div slot="modal-footer" class="modal-footer">
      <button type="button" class="btn btn-default" @click='removeChart'>Yes</button>
      <button type="button" class="btn btn-success" @click='showDeletionConfirmModal = false'>No</button>
    </div>
  </modal>


</template>

<style scoped>
  .no-border {
    border:none;
  }
  .control-bar {
    float:none;
    text-align: left;
    margin-right: 5%;
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
  import {modal} from 'vue-strap'

  export default {
    props: ['options', 'theme','showConfig','currentConfig'],
    components:{
      'lcharts':Lcharts,
       modal
    },
    data: function () {
      return {
        chart: null,
        showChartControlBar:false,
        showDeletionConfirmModal:false,
        showDeletionCompleteAlert:false
      }
    },
    methods: {
      openConfiguration: function(){
        this.showConfig = true;
        this.currentConfig = this.options;
      },
      removeChart : function(){
        this.showDeletionCompleteAlert = true;
        //ask lchart to destroy chart firstly
        this.$broadcast('dispose-chart',this.options);
        //ask parent Chartpage to remove the chart segment
        this.$dispatch('remove-chart',this.options);

      },
  }
  }
</script>
