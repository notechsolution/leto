<template>
    <div :id='id'>
      <template v-for="chartSegment in chartSegments">
          <lcharts :options='chartSegment'></lcharts>
      </template>
    </div>
</template>
<style>

</style>
<script>
    import Lcharts from './Lcharts.vue'
    import SampleUtils from '../utils/SampleUtils'

    export default{
        data(){
            return{
              chartSegments:SampleUtils.demoChartConfigs,
              pageOptions: {}
            }
        },
        components:{
            'lcharts':Lcharts
        },
        props:['id']
    }
</script>
