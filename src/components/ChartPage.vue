<template>
    <div :id='id'>
      <template v-for="chartSegment in chartSegments">
          <chart-segment :options='chartSegment' :show-config.sync='showConfig' :current-config.sync='currentConfig' :id='id'></chart-segment>
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
    <p>You successfully delete the chart '{{currentConfig.title.text}}'.</p>
  </alert>

  <modal :show.sync="showDeletionConfirmModal" effect="fade">
    <div slot="modal-header" class="modal-header">
      <h4 class="modal-title">
        Delete Confirmation
      </h4>
    </div>
    <div slot="modal-body" class="modal-body">Do you want to <b>DELETE</b> the chart '{{currentConfig.title.text}}'? It cannot Undo</div>
    <div slot="modal-footer" class="modal-footer">
      <button type="button" class="btn btn-default" @click='removeChart'>Yes</button>
      <button type="button" class="btn btn-success" @click='showDeletionConfirmModal = false'>No</button>
    </div>
  </modal>

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
              showDeletionCompleteAlert:false,
              showDeletionConfirmModal:false
            }
        },
        components:{
          ChartSegment,
          modal,
          ChartOptions,
          alert
        },
        events :{
         'open-deletion-modal': function(chartOptions){
            this.currentConfig = chartOptions;
            this.showDeletionConfirmModal = true;
          }
        },
      methods : {
        removeChart: function(){
          //ask chartSegment->lchart to destroy chart firstly
          this.$broadcast('dispose-chart',this.currentConfig);
          this.chartSegments.$remove(this.currentConfig);
          this.showDeletionCompleteAlert = true;
          this.showDeletionConfirmModal = false;
        }
      },
        props:['id']
    }
</script>
