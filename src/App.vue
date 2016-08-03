<template>
  <div id="app" >
    <lcharts :options='polar'></lcharts>
    <!--<lcharts :options='chinaMovement'></lcharts>-->
    <lcharts :options='bar' v-ref:bar></lcharts>
    <lcharts :options='worldMap'></lcharts>
  </div>
</template>

<script>
import Hello from './components/Hello'
import Lcharts from './components/Lcharts.vue'
import echarts from 'echarts'
import world from 'echarts/map/js/world';
import china from 'echarts/map/js/china';

export default {
  components: {
    Hello,
    Lcharts
  },
  data: function () {
    let data = []
    for (let i = 0; i <= 360; i++) {
      let t = i / 180 * Math.PI;
      let r = Math.sin(2 * t) * Math.cos(2 * t);
      data.push([r, i]);
    }
    return {
      polar: {
        title: {
          text: '极坐标双数值轴'
        },
        legend: {
          data: ['line']
        },
        polar: {
          center: ['50%', '54%']
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          }
        },
        angleAxis: {
          type: 'value',
          startAngle: 0
        },
        radiusAxis: {
          min: 0
        },
        series: [
          {
            coordinateSystem: 'polar',
            name: 'line',
            type: 'line',
            showSymbol: false,
            data: data
          }
        ],
        animationDuration: 2000
      },
      bar: {
        title: {
          text: '异步数据加载示例'
        },
        tooltip: {},
        legend: {
          data:['销量']
        },
        xAxis: {
          data: []
        },
        yAxis: {},
        series: [{
          name: '销量',
          type: 'bar',
          data: []
        }]
      },
      worldMap:{
        title: {
          text: 'World Population (2010)',
          subtext: 'from United Nations, Total population, both sexes combined, as of 1 July (thousands)',
          sublink: 'http://esa.un.org/wpp/Excel-Data/population.htm',
          left: 'center',
          top: 'top'
        },
        tooltip: {
          trigger: 'item',
          formatter: function (params) {
            var value = (params.value + '').split('.');
            value = value[0].replace(/(\d{1,3})(?=(?:\d{3})+(?!\d))/g, '$1,')
              + '.' + value[1];
            return params.seriesName + '<br/>' + params.name + ' : ' + value;
          }
        },
        toolbox: {
          show: true,
          orient: 'vertical',
          left: 'right',
          top: 'center',
          feature: {
            dataView: {readOnly: false},
            restore: {},
            saveAsImage: {}
          }
        },
        visualMap: {
          min: 0,
          max: 1000000,
          text:['High','Low'],
          realtime: false,
          calculable: true,
          inRange: {
            color: ['lightskyblue','yellow', 'orangered']
          }
        },
        series: [
          {
            name: 'World Population (2010)',
            type: 'map',
            mapType: 'world',
            roam: true,
            itemStyle:{
              emphasis:{label:{show:true}}
            },
            data:[
              {name: 'Afghanistan', value: 28397.812},
              {name: 'Angola', value: 19549.124},
              {name: 'Albania', value: 3150.143},
              {name: 'United Arab Emirates', value: 8441.537},
              {name: 'Argentina', value: 40374.224},
              {name: 'Armenia', value: 2963.496},
              {name: 'French Southern and Antarctic Lands', value: 268.065},
              {name: 'Australia', value: 22404.488},
              {name: 'Austria', value: 8401.924},
              {name: 'Azerbaijan', value: 9094.718},
              {name: 'Burundi', value: 9232.753},
              {name: 'Belgium', value: 10941.288},
              {name: 'Benin', value: 9509.798},
              {name: 'Burkina Faso', value: 15540.284},
              {name: 'Bangladesh', value: 151125.475},
              {name: 'Bulgaria', value: 7389.175},
              {name: 'The Bahamas', value: 66402.316},
              {name: 'Bosnia and Herzegovina', value: 3845.929},
              {name: 'Belarus', value: 9491.07},
              {name: 'Belize', value: 308.595},
              {name: 'Bermuda', value: 64.951},
              {name: 'Bolivia', value: 716.939},
              {name: 'Brazil', value: 195210.154},
              {name: 'Brunei', value: 27.223},
              {name: 'Bhutan', value: 716.939},
              {name: 'Botswana', value: 1969.341},
              {name: 'Central African Republic', value: 4349.921},
              {name: 'Canada', value: 34126.24},
              {name: 'Switzerland', value: 7830.534},
              {name: 'Chile', value: 17150.76},
              {name: 'China', value: 1359821.465},
              {name: 'Ivory Coast', value: 60508.978},
              {name: 'Cameroon', value: 20624.343},
              {name: 'Democratic Republic of the Congo', value: 62191.161},
              {name: 'Republic of the Congo', value: 3573.024},
              {name: 'Colombia', value: 46444.798},
              {name: 'Costa Rica', value: 4669.685},
              {name: 'Cuba', value: 11281.768},
              {name: 'Northern Cyprus', value: 1.468},
              {name: 'Cyprus', value: 1103.685},
              {name: 'Czech Republic', value: 10553.701},
              {name: 'Germany', value: 83017.404},
              {name: 'Djibouti', value: 834.036},
              {name: 'Denmark', value: 5550.959},
              {name: 'Dominican Republic', value: 10016.797},
              {name: 'Algeria', value: 37062.82},
              {name: 'Ecuador', value: 15001.072},
              {name: 'Egypt', value: 78075.705},
              {name: 'Eritrea', value: 5741.159},
              {name: 'Spain', value: 46182.038},
              {name: 'Estonia', value: 1298.533},
              {name: 'Ethiopia', value: 87095.281},
              {name: 'Finland', value: 5367.693},
              {name: 'Fiji', value: 860.559},
              {name: 'Falkland Islands', value: 49.581},
              {name: 'France', value: 63230.866},
              {name: 'Gabon', value: 1556.222},
              {name: 'United Kingdom', value: 62066.35},
              {name: 'Georgia', value: 4388.674},
              {name: 'Ghana', value: 24262.901},
              {name: 'Guinea', value: 10876.033},
              {name: 'Gambia', value: 1680.64},
              {name: 'Guinea Bissau', value: 10876.033},
              {name: 'Equatorial Guinea', value: 696.167},
              {name: 'Greece', value: 11109.999},
              {name: 'Greenland', value: 56.546},
              {name: 'Guatemala', value: 14341.576},
              {name: 'French Guiana', value: 231.169},
              {name: 'Guyana', value: 786.126},
              {name: 'Honduras', value: 7621.204},
              {name: 'Croatia', value: 4338.027},
              {name: 'Haiti', value: 9896.4},
              {name: 'Hungary', value: 10014.633},
              {name: 'Indonesia', value: 240676.485},
              {name: 'India', value: 1205624.648},
              {name: 'Ireland', value: 4467.561},
              {name: 'Iran', value: 240676.485},
              {name: 'Iraq', value: 30962.38},
              {name: 'Iceland', value: 318.042},
              {name: 'Israel', value: 7420.368},
              {name: 'Italy', value: 60508.978},
              {name: 'Jamaica', value: 2741.485},
              {name: 'Jordan', value: 6454.554},
              {name: 'Japan', value: 127352.833},
              {name: 'Kazakhstan', value: 15921.127},
              {name: 'Kenya', value: 40909.194},
              {name: 'Kyrgyzstan', value: 5334.223},
              {name: 'Cambodia', value: 14364.931},
              {name: 'South Korea', value: 51452.352},
              {name: 'Kosovo', value: 97.743},
              {name: 'Kuwait', value: 2991.58},
              {name: 'Laos', value: 6395.713},
              {name: 'Lebanon', value: 4341.092},
              {name: 'Liberia', value: 3957.99},
              {name: 'Libya', value: 6040.612},
              {name: 'Sri Lanka', value: 20758.779},
              {name: 'Lesotho', value: 2008.921},
              {name: 'Lithuania', value: 3068.457},
              {name: 'Luxembourg', value: 507.885},
              {name: 'Latvia', value: 2090.519},
              {name: 'Morocco', value: 31642.36},
              {name: 'Moldova', value: 103.619},
              {name: 'Madagascar', value: 21079.532},
              {name: 'Mexico', value: 117886.404},
              {name: 'Macedonia', value: 507.885},
              {name: 'Mali', value: 13985.961},
              {name: 'Myanmar', value: 51931.231},
              {name: 'Montenegro', value: 620.078},
              {name: 'Mongolia', value: 2712.738},
              {name: 'Mozambique', value: 23967.265},
              {name: 'Mauritania', value: 3609.42},
              {name: 'Malawi', value: 15013.694},
              {name: 'Malaysia', value: 28275.835},
              {name: 'Namibia', value: 2178.967},
              {name: 'New Caledonia', value: 246.379},
              {name: 'Niger', value: 15893.746},
              {name: 'Nigeria', value: 159707.78},
              {name: 'Nicaragua', value: 5822.209},
              {name: 'Netherlands', value: 16615.243},
              {name: 'Norway', value: 4891.251},
              {name: 'Nepal', value: 26846.016},
              {name: 'New Zealand', value: 4368.136},
              {name: 'Oman', value: 2802.768},
              {name: 'Pakistan', value: 173149.306},
              {name: 'Panama', value: 3678.128},
              {name: 'Peru', value: 29262.83},
              {name: 'Philippines', value: 93444.322},
              {name: 'Papua New Guinea', value: 6858.945},
              {name: 'Poland', value: 38198.754},
              {name: 'Puerto Rico', value: 3709.671},
              {name: 'North Korea', value: 1.468},
              {name: 'Portugal', value: 10589.792},
              {name: 'Paraguay', value: 6459.721},
              {name: 'Qatar', value: 1749.713},
              {name: 'Romania', value: 21861.476},
              {name: 'Russia', value: 21861.476},
              {name: 'Rwanda', value: 10836.732},
              {name: 'Western Sahara', value: 514.648},
              {name: 'Saudi Arabia', value: 27258.387},
              {name: 'Sudan', value: 35652.002},
              {name: 'South Sudan', value: 9940.929},
              {name: 'Senegal', value: 12950.564},
              {name: 'Solomon Islands', value: 526.447},
              {name: 'Sierra Leone', value: 5751.976},
              {name: 'El Salvador', value: 6218.195},
              {name: 'Somaliland', value: 9636.173},
              {name: 'Somalia', value: 9636.173},
              {name: 'Republic of Serbia', value: 3573.024},
              {name: 'Suriname', value: 524.96},
              {name: 'Slovakia', value: 5433.437},
              {name: 'Slovenia', value: 2054.232},
              {name: 'Sweden', value: 9382.297},
              {name: 'Swaziland', value: 1193.148},
              {name: 'Syria', value: 7830.534},
              {name: 'Chad', value: 11720.781},
              {name: 'Togo', value: 6306.014},
              {name: 'Thailand', value: 66402.316},
              {name: 'Tajikistan', value: 7627.326},
              {name: 'Turkmenistan', value: 5041.995},
              {name: 'East Timor', value: 10016.797},
              {name: 'Trinidad and Tobago', value: 1328.095},
              {name: 'Tunisia', value: 10631.83},
              {name: 'Turkey', value: 72137.546},
              {name: 'United Republic of Tanzania', value: 44973.33},
              {name: 'Uganda', value: 33987.213},
              {name: 'Ukraine', value: 46050.22},
              {name: 'Uruguay', value: 3371.982},
              {name: 'United States of America', value: 312247.116},
              {name: 'Uzbekistan', value: 27769.27},
              {name: 'Venezuela', value: 236.299},
              {name: 'Vietnam', value: 89047.397},
              {name: 'Vanuatu', value: 236.299},
              {name: 'West Bank', value: 13.565},
              {name: 'Yemen', value: 22763.008},
              {name: 'South Africa', value: 51452.352},
              {name: 'Zambia', value: 13216.985},
              {name: 'Zimbabwe', value: 13076.978}
            ]
          }
        ]
      },
      chinaMovement:{
        backgroundColor: '#404a59',
        title : {
          text: '模拟迁徙',
          subtext: '数据纯属有影无迹',
          left: 'center',
          textStyle : {
            color: '#fff'
          }
        },
        tooltip : {
          trigger: 'item'
        },
        legend: {
          orient: 'vertical',
          top: 'bottom',
          left: 'right',
          data:['北京 Top10', '上海 Top10', '广州 Top10'],
          textStyle: {
            color: '#fff'
          },
          selectedMode: 'single'
        },
        geo: {
          map: 'china',
          label: {
            emphasis: {
              show: false
            }
          },
          roam: true,
          itemStyle: {
            normal: {
              areaColor: '#323c48',
              borderColor: '#404a59'
            },
            emphasis: {
              areaColor: '#2a333d'
            }
          }
        },
        series: series
      }
    }
  },
  ready: function(){
// simulating async data from server
    setTimeout(() => {
      this.$refs.bar.mergeOptions({
      xAxis: {
        data: asyncData.categories
      },
      series: [{
        name: '销量',
        data: asyncData.data
      }]
    })
  }, 3000)
  }
}

  //supporting data
let asyncData = {
  categories: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"],
  data: [5, 20, 36, 10, 10, 20]
}
var geoCoordMap = {
  '上海': [121.4648,31.2891],
  '东莞': [113.8953,22.901],
  '东营': [118.7073,37.5513],
  '中山': [113.4229,22.478],
  '临汾': [111.4783,36.1615],
  '临沂': [118.3118,35.2936],
  '丹东': [124.541,40.4242],
  '丽水': [119.5642,28.1854],
  '乌鲁木齐': [87.9236,43.5883],
  '佛山': [112.8955,23.1097],
  '保定': [115.0488,39.0948],
  '兰州': [103.5901,36.3043],
  '包头': [110.3467,41.4899],
  '北京': [116.4551,40.2539],
  '北海': [109.314,21.6211],
  '南京': [118.8062,31.9208],
  '南宁': [108.479,23.1152],
  '南昌': [116.0046,28.6633],
  '南通': [121.1023,32.1625],
  '厦门': [118.1689,24.6478],
  '台州': [121.1353,28.6688],
  '合肥': [117.29,32.0581],
  '呼和浩特': [111.4124,40.4901],
  '咸阳': [108.4131,34.8706],
  '哈尔滨': [127.9688,45.368],
  '唐山': [118.4766,39.6826],
  '嘉兴': [120.9155,30.6354],
  '大同': [113.7854,39.8035],
  '大连': [122.2229,39.4409],
  '天津': [117.4219,39.4189],
  '太原': [112.3352,37.9413],
  '威海': [121.9482,37.1393],
  '宁波': [121.5967,29.6466],
  '宝鸡': [107.1826,34.3433],
  '宿迁': [118.5535,33.7775],
  '常州': [119.4543,31.5582],
  '广州': [113.5107,23.2196],
  '廊坊': [116.521,39.0509],
  '延安': [109.1052,36.4252],
  '张家口': [115.1477,40.8527],
  '徐州': [117.5208,34.3268],
  '德州': [116.6858,37.2107],
  '惠州': [114.6204,23.1647],
  '成都': [103.9526,30.7617],
  '扬州': [119.4653,32.8162],
  '承德': [117.5757,41.4075],
  '拉萨': [91.1865,30.1465],
  '无锡': [120.3442,31.5527],
  '日照': [119.2786,35.5023],
  '昆明': [102.9199,25.4663],
  '杭州': [119.5313,29.8773],
  '枣庄': [117.323,34.8926],
  '柳州': [109.3799,24.9774],
  '株洲': [113.5327,27.0319],
  '武汉': [114.3896,30.6628],
  '汕头': [117.1692,23.3405],
  '江门': [112.6318,22.1484],
  '沈阳': [123.1238,42.1216],
  '沧州': [116.8286,38.2104],
  '河源': [114.917,23.9722],
  '泉州': [118.3228,25.1147],
  '泰安': [117.0264,36.0516],
  '泰州': [120.0586,32.5525],
  '济南': [117.1582,36.8701],
  '济宁': [116.8286,35.3375],
  '海口': [110.3893,19.8516],
  '淄博': [118.0371,36.6064],
  '淮安': [118.927,33.4039],
  '深圳': [114.5435,22.5439],
  '清远': [112.9175,24.3292],
  '温州': [120.498,27.8119],
  '渭南': [109.7864,35.0299],
  '湖州': [119.8608,30.7782],
  '湘潭': [112.5439,27.7075],
  '滨州': [117.8174,37.4963],
  '潍坊': [119.0918,36.524],
  '烟台': [120.7397,37.5128],
  '玉溪': [101.9312,23.8898],
  '珠海': [113.7305,22.1155],
  '盐城': [120.2234,33.5577],
  '盘锦': [121.9482,41.0449],
  '石家庄': [114.4995,38.1006],
  '福州': [119.4543,25.9222],
  '秦皇岛': [119.2126,40.0232],
  '绍兴': [120.564,29.7565],
  '聊城': [115.9167,36.4032],
  '肇庆': [112.1265,23.5822],
  '舟山': [122.2559,30.2234],
  '苏州': [120.6519,31.3989],
  '莱芜': [117.6526,36.2714],
  '菏泽': [115.6201,35.2057],
  '营口': [122.4316,40.4297],
  '葫芦岛': [120.1575,40.578],
  '衡水': [115.8838,37.7161],
  '衢州': [118.6853,28.8666],
  '西宁': [101.4038,36.8207],
  '西安': [109.1162,34.2004],
  '贵阳': [106.6992,26.7682],
  '连云港': [119.1248,34.552],
  '邢台': [114.8071,37.2821],
  '邯郸': [114.4775,36.535],
  '郑州': [113.4668,34.6234],
  '鄂尔多斯': [108.9734,39.2487],
  '重庆': [107.7539,30.1904],
  '金华': [120.0037,29.1028],
  '铜川': [109.0393,35.1947],
  '银川': [106.3586,38.1775],
  '镇江': [119.4763,31.9702],
  '长春': [125.8154,44.2584],
  '长沙': [113.0823,28.2568],
  '长治': [112.8625,36.4746],
  '阳泉': [113.4778,38.0951],
  '青岛': [120.4651,36.3373],
  '韶关': [113.7964,24.7028]
};

var BJData = [
  [{name:'北京'}, {name:'上海',value:95}],
  [{name:'北京'}, {name:'广州',value:90}],
  [{name:'北京'}, {name:'大连',value:80}],
  [{name:'北京'}, {name:'南宁',value:70}],
  [{name:'北京'}, {name:'南昌',value:60}],
  [{name:'北京'}, {name:'拉萨',value:50}],
  [{name:'北京'}, {name:'长春',value:40}],
  [{name:'北京'}, {name:'包头',value:30}],
  [{name:'北京'}, {name:'重庆',value:20}],
  [{name:'北京'}, {name:'常州',value:10}]
];

var SHData = [
  [{name:'上海'},{name:'包头',value:95}],
  [{name:'上海'},{name:'昆明',value:90}],
  [{name:'上海'},{name:'广州',value:80}],
  [{name:'上海'},{name:'郑州',value:70}],
  [{name:'上海'},{name:'长春',value:60}],
  [{name:'上海'},{name:'重庆',value:50}],
  [{name:'上海'},{name:'长沙',value:40}],
  [{name:'上海'},{name:'北京',value:30}],
  [{name:'上海'},{name:'丹东',value:20}],
  [{name:'上海'},{name:'大连',value:10}]
];

var GZData = [
  [{name:'广州'},{name:'福州',value:95}],
  [{name:'广州'},{name:'太原',value:90}],
  [{name:'广州'},{name:'长春',value:80}],
  [{name:'广州'},{name:'重庆',value:70}],
  [{name:'广州'},{name:'西安',value:60}],
  [{name:'广州'},{name:'成都',value:50}],
  [{name:'广州'},{name:'常州',value:40}],
  [{name:'广州'},{name:'北京',value:30}],
  [{name:'广州'},{name:'北海',value:20}],
  [{name:'广州'},{name:'海口',value:10}]
];

var planePath = 'path://M1705.06,1318.313v-89.254l-319.9-221.799l0.073-208.063c0.521-84.662-26.629-121.796-63.961-121.491c-37.332-0.305-64.482,36.829-63.961,121.491l0.073,208.063l-319.9,221.799v89.254l330.343-157.288l12.238,241.308l-134.449,92.931l0.531,42.034l175.125-42.917l175.125,42.917l0.531-42.034l-134.449-92.931l12.238-241.308L1705.06,1318.313z';

var convertData = function (data) {
  var res = [];
  for (var i = 0; i < data.length; i++) {
    var dataItem = data[i];
    var fromCoord = geoCoordMap[dataItem[0].name];
    var toCoord = geoCoordMap[dataItem[1].name];
    if (fromCoord && toCoord) {
      res.push({
        fromName: dataItem[0].name,
        toName: dataItem[1].name,
        coords: [fromCoord, toCoord]
      });
    }
  }
  return res;
};

var color = ['#a6c84c', '#ffa022', '#46bee9'];
var series = [];
[['北京', BJData], ['上海', SHData], ['广州', GZData]].forEach(function (item, i) {
  series.push({
      name: item[0] + ' Top10',
      type: 'lines',
      zlevel: 1,
      effect: {
        show: true,
        period: 6,
        trailLength: 0.7,
        color: '#fff',
        symbolSize: 3
      },
      lineStyle: {
        normal: {
          color: color[i],
          width: 0,
          curveness: 0.2
        }
      },
      data: convertData(item[1])
    },
    {
      name: item[0] + ' Top10',
      type: 'lines',
      zlevel: 2,
      effect: {
        show: true,
        period: 6,
        trailLength: 0,
        symbol: planePath,
        symbolSize: 15
      },
      lineStyle: {
        normal: {
          color: color[i],
          width: 1,
          opacity: 0.4,
          curveness: 0.2
        }
      },
      data: convertData(item[1])
    },
    {
      name: item[0] + ' Top10',
      type: 'effectScatter',
      coordinateSystem: 'geo',
      zlevel: 2,
      rippleEffect: {
        brushType: 'stroke'
      },
      label: {
        normal: {
          show: true,
          position: 'right',
          formatter: '{b}'
        }
      },
      symbolSize: function (val) {
        return val[2] / 8;
      },
      itemStyle: {
        normal: {
          color: color[i]
        }
      },
      data: item[1].map(function (dataItem) {
        return {
          name: dataItem[1].name,
          value: geoCoordMap[dataItem[1].name].concat([dataItem[1].value])
        };
      })
    });
});

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
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
