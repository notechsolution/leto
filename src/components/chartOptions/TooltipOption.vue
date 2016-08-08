<template>
  <div class="row">
    <span>I am {{optionName}} configuration page -- Tooltip</span>
  </div>
</template>
<style>

</style>
<script>
  export default{
    data(){
      return {
        tabName:'title'
      }
    },
    computed: {
      // a computed getter
      configJSON: function () {
        return JSON.stringify(this.chartOptions, null, 2).substring(0, 1000) + '...';
      }
    },
    methods:{
      clickTag :function(tag){
        this.currentTag = tag;
      }
    },
    props: ['chartOptions','optionName']
  }
</script>
