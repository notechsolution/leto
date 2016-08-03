<template>
  <div class="col-md-3">
    <ul class="nav nav-pills nav-stacked">
      <li v-bind:class="currentTab=='general'?active:''" v-on:click='currentTab="general"'><a href="#">General</a></li>
      <li v-bind:class="currentTab=='title'?active:''" v-on:click='currentTab="title"'><a href="#">Title</a></li>
      <li v-bind:class="currentTab=='canvas'?active:''" v-on:click='currentTab="canvas"'><a href="#">Canvas</a></li>
      <li v-bind:class="currentTab=='xaxes'?active:''" v-on:click='currentTab="xaxes"'><a href="#">X-Axes</a></li>
      <li v-bind:class="currentTab=='yaxes'?active:''" v-on:click='currentTab="yaxes"'><a href="#">Y-Axes</a></li>
      <li v-bind:class="currentTab=='legend'?active:''" v-on:click='currentTab="legend"'><a href="#">Legend</a></li>
      <li v-bind:class="currentTab=='tooltip'?active:''" v-on:click='currentTab="tooltip"'><a href="#">Tooltip</a></li>
      <li v-bind:class="currentTab=='tools'?active:''" v-on:click='currentTab="tools"'><a href="#">Tools</a></li>
    </ul>
  </div>
  <div class="col-md-9">
    {{currentTag}}:<br/>{{configJSON}}
  </div>
</template>
<style>

</style>
<script>
  export default{
    data(){
      return {
        currentTab:'general'
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
