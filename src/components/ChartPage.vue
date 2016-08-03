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
      <div slot="modal-body" class="modal-body row">
        <chart-options :options='currentConfig'></chart-options>
      </div>
  </modal>
</template>
<style>

</style>
<script>
    import ChartSegment from './ChartSegment.vue'
    import SampleUtils from '../utils/SampleUtils'
    import {modal} from 'vue-strap'
    import ChartOptions from './chartOptions/ChartOptions.vue'

    export default{
        data(){
            return{
              chartSegments:SampleUtils.demoChartConfigs,
              pageOptions: {},
              showConfig : false,
              showChartControlBar:false,
              currentConfig:{}
            }
        },
        components:{
          ChartSegment,
          modal,
          ChartOptions
        },
        props:['id']
    }
</script>
