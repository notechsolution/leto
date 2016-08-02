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
      <div slot="modal-body" class="modal-body">{{configJSON}}</div>
  </modal>
</template>
<style>

</style>
<script>
    import ChartSegment from './ChartSegment.vue'
    import SampleUtils from '../utils/SampleUtils'
    import {modal} from 'vue-strap'

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
             modal
        },
        computed: {
          // a computed getter
          configJSON: function () {
            return JSON.stringify(this.currentConfig,null,2).substring(0,1000)+'...';
          }
        },
        props:['id']
    }
</script>
