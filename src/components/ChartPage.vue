<template>
    <div :id='id'>
      <template v-for="chartSegment in chartSegments">
          <chart-segment :options='chartSegment' :show-config.sync='showConfig' :current-config.sync='currentConfig'></chart-segment>
      </template>
    </div>
  <modal :show.sync='showConfig' effect='fade'>
    <div slot="modal-header" class="modal-header">
      <h4 class="modal-title">Configuration Page</h4>
    </div>
      <div slot="modal-body" class="modal-body body-tabs">
        <chart-options :options='currentConfig'></chart-options>
      </div>
  </modal>

  <alert :show.sync="showDeletionCompleteAlert" :duration="3000" type="success" placement="top-right" dismissable>
    <span class="icon-ok-circled alert-icon-float-left"></span>
    <strong>Deletion Done!</strong>
    <p>You successfully delete the chart.</p>
  </alert>
</template>
<style>
.body-tabs {
  padding: 0 15px 0 15px !important;
}
</style>
<script>
    import ChartSegment from './ChartSegment.vue'
    import SampleUtils from '../utils/SampleUtils'
    import {modal} from 'vue-strap'
    import ChartOptions from './chartOptions/ChartOptions.vue'
    import {alert} from 'vue-strap'

    export default{
        data(){
            return{
              chartSegments:SampleUtils.demoChartConfigs,
              pageOptions: {},
              showConfig : false,
              showChartControlBar:false,
              currentConfig:{},
              showDeletionCompleteAlert:false
            }
        },
        components:{
          ChartSegment,
          modal,
          ChartOptions,
          alert
        },
        events :{
          'remove-chart': function(chartOptions){
            this.chartSegments.$remove(chartOptions);
            this.showDeletionCompleteAlert = true;
          }
        },
        props:['id']
    }
</script>
