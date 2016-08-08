<template>
  <div class="row bhoechie-tab-container">
  <div class="col-md-3 bhoechie-tab-menu">
    <div class="list-group">
      <template v-for='tab in tabs'>
        <a href="#"  v-bind:class="['list-group-item','text-center',currentTab==tab?'active':'']"  v-on:click='currentTab=tab'>
          {{tab}}
        </a>
      </template>
    </div>
  </div>
  <div class="col-md-9 bhoechie-tab">
   <!--<general-option :chart-options.sync='options' option-name='general' v-show='currentTab=="General"'></general-option>-->
   <!--<title-option :chart-options.sync='options' option-name='title' v-show='currentTab=="Title"'></title-option>-->

    <component :is="currentTab" :chart-options.sync='options' :option-name='currentTab'>
      <!-- component changes when vm.currentTab changes! -->
    </component>

  </div>
    </div>
</template>
<style>
@import '../../assets/css/vertical-tab.css';
</style>
<script>
  import GeneralOption from './GeneralOption.vue'
  import TitleOption from  './TitleOption.vue'
  import CanvasOption from  './CanvasOption.vue'
  import AxesOption from  './AxesOption.vue'
  import LegendOption from  './LegendOption.vue'
  import TooltipOption from  './TooltipOption.vue'
  import ToolsOption from  './ToolsOption.vue'

  export default{
    components:{
      'General':GeneralOption,
      'Title':TitleOption,
      'Canvas' :CanvasOption,
      'X-Axes':AxesOption,
      'Y-Axes':AxesOption,
      'Legend':LegendOption,
      'Tooltip':TooltipOption,
      'Tools':ToolsOption
    },
    data(){
      return {
        currentTab:'General',
        tabs:['General','Title','Canvas','X-Axes','Y-Axes','Legend','Tooltip','Tools']
      }
    },
    computed: {
      // a computed getter
      configJSON: function () {
        return JSON.stringify(this.options, null, 2).substring(0, 1000) + '...';
      }
    },
    methods:{
      clickTag :function(tag){
        this.currentTag = tag;
      }
    },
    props: ['options']
  }
</script>
