<template>
  <div id="app" >
    <chart-page :id='pageId'></chart-page>
    <!--<hello></hello>-->
  </div>
</template>

<script>
import ChartPage from './components/ChartPage.vue'
import world from 'echarts/map/js/world';
import china from 'echarts/map/js/china';
import Hello from './components/Hello.vue'

export default {
  components: {
    ChartPage,
    Hello
  },
  data: function () {
    return {
      pageId:'page001'
    }
  },
  ready: function(){
  }
}

</script>

<style>
html {
  height: 100%;
}

body {
  display:flex;
  align-items: left;
  justify-content: left;
  height: 100%;
}

#app {
  color: #2c3e50;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
