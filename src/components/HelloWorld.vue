<template>
  <div id="helloword">
    <div class="wrapper">
      <div style="" id="zhuxingtu"></div>
      <div style="" id="zhuxingtu2"></div>
      <div style="clear:both"></div>
    </div>
    <div  class="wrapper">
      <div style="" id="shanxingtu"></div>
      <div style="" id="huanxingtu"></div>
      <div style="clear:both"></div>
    </div>
    <div class="wrapper">
      <div id="map"></div>
      <div style="clear:both"></div>
    </div>
    <div id="map2"></div>
    
  </div>
</template>
<script>
  import china from '../../static/china.js'
  export default {
    data() {
      return {
          charts: '',
            opinion:['直接访问','邮件营销','联盟广告','视频广告','搜索引擎'],
            opinionData:[
              {value:335, name:'直接访问'},
              {value:310, name:'邮件营销'},
              {value:234, name:'联盟广告'},
              {value:135, name:'视频广告'},
              {value:1548, name:'搜索引擎'}
            ]
      }
    }, 
    methods:{
      initEchart(){

        // 绘制柱形图1
        var myChartZhu = this.$echarts.init(document.getElementById('zhuxingtu'));
        myChartZhu.setOption({
          backgroundColor: '#e6e2e4',
          title: {
            text: 'ECharts 单一表格示例'
          },
          tooltip: {},
          xAxis: {
            data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
          },
          yAxis: {},
          series: [{
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
          }]
        });

        // 绘制柱形图2
        var myChartZhu2 = this.$echarts.init(document.getElementById('zhuxingtu2'));
        myChartZhu2.setOption({
          backgroundColor: '#e6e2e4',
          title: {
            text: 'ECharts 多表表格示例'
          },
          legend: {},
          tooltip: {},
          dataset: {
              // 提供一份数据。
              source: [
                  ['product', '2015', '2016', '2017'],
                  ['Matcha Latte', 43.3, 85.8, 93.7],
                  ['Milk Tea', 83.1, 73.4, 55.1],
                  ['Cheese Cocoa', 86.4, 65.2, 82.5],
                  ['Walnut Brownie', 72.4, 53.9, 39.1]
              ]
          },
          // 声明一个 X 轴，类目轴（category）。默认情况下，类目轴对应到 dataset 第一列。
          xAxis: {type: 'category'},
          // 声明一个 Y 轴，数值轴。
          yAxis: {},
          // 声明多个 bar 系列，默认情况下，每个系列会自动对应到 dataset 的每一列。
          series: [
              {type: 'bar'},
              {type: 'bar'},
              {type: 'bar'}
          ]
        });

        // 绘制扇形图
        var myChartShan = this.$echarts.init(document.getElementById('shanxingtu'));
        myChartShan.setOption({
          backgroundColor: '#e6e2e4',
          textStyle: {
            // color: '#000',//显示扇形图标题
            fontWeight:'bold',//字体加粗
            fontSize:'18'
          },
          color: ['#000','rgb(252,157,154)','rgb(249,205,173)','rgb(200,200,169)','rgb(131,175,155)'],
          series : [
            {
              name: '访问来源',
              type: 'pie',
              radius: '60%',
              data:[
                {value:235, name:'视频广告'},
                {value:274, name:'联盟广告'},
                {value:310, name:'邮件营销'},
                {value:335, name:'直接访问'},
                {value:400, name:'搜索引擎'}
              ],

            }
          ],
        });

        // 绘制环形图
        var myChartHuan = this.$echarts.init(document.getElementById('huanxingtu'));
        myChartHuan.setOption({
           backgroundColor: '#e6e2e4',
           tooltip: {
            trigger: 'item',
             formatter: '{a}<br/>{b}:{c} ({d}%)'
           },
           legend: {
             orient: 'vertical',
             x: 'left',
             data:this.opinion
           },
           series: [
             { 
               name:'访问来源',
               type:'pie',
               radius:['40%','70%'],
               avoidLabelOverlap: false,
               label: {
                 normal: {
                   show: false,
                   position: 'center',
                 },
                 emphasis: {
                   show: true,
                   textStyle: {
                     fontSize: '30',
                     fontWeight: 'blod'
                   }
                 }
               },
               labelLine: {
                 normal: {
                   show: false
                 }
               },
               data:this.opinionData
             }
           ]
        });
        // 绘制地图1
        var myChartMap = this.$echarts.init(document.getElementById('map'));
        myChartMap.setOption({
          backgroundColor: '#e6e2e4',
          title : {
            text: '订单量',
            subtext: '纯属虚构',
            x:'center'
          },
          tooltip : {
            trigger: 'item'
          },
          legend: {
            orient: 'vertical',
            x:'left',
            data:['订单量']
          },
          visualMap: {
            type: 'piecewise',
            pieces: [
              {min: 1500},
              {min: 900, max: 1500},
              {min: 310, max: 1000},
              {min: 200, max: 300},
              {min: 10, max: 200, label: '10 到 200（自定义label）'},
              {value: 123, label: '123（自定义特殊颜色）', color: 'grey'},
              {min: 5, max: 5, label: '5（自定义特殊颜色）', color: 'black'},
              {max: 5}
            ],
            color: ['#E0022B', '#E09107', '#A3E00B']
          },
          // 工具盒，可以保存图片
          toolbox: {
            show: true,
            orient : 'vertical',
            x: 'right',
            y: 'center',
            feature : {
              mark : {show: true},
              dataView : {show: true, readOnly: false},
              restore : {show: true},
              saveAsImage : {show: true}
            }
          },
          roamController: {
            show: true,
            x: 'right',
            mapTypeControl: {
                'china': true
            }
          },
          series : [{
              name: '订单量',
              type: 'map',
              mapType: 'china',
              roam: false,
              itemStyle:{
                normal:{
                  label:{
                    show:true,
                    textStyle: {
                       color: "#fff"
                    }
                  },
                  areaColor: '#323c48',//地图区域的颜色
                  borderColor: '#000'//图形的描边颜色
                },
                emphasis:{
                  label:{
                    show:false
                  }
                }
              },
            data:[
              {name: '北京',value: 5},
              {name: '天津',value: Math.round(Math.random()*2000)},
              {name: '上海',value: Math.round(Math.random()*2000)},
              {name: '重庆',value: Math.round(Math.random()*2000)},
              {name: '河北',value: 0},
              {name: '河南',value: Math.round(Math.random()*2000)},
              {name: '云南',value: 123},
              {name: '辽宁',value: 305},
              {name: '黑龙江',value: Math.round(Math.random()*2000)},
              {name: '湖南',value: 200},
              {name: '安徽',value: Math.round(Math.random()*2000)},
              {name: '山东',value: Math.round(Math.random()*2000)},
              {name: '新疆',value: Math.round(Math.random()*2000)},
              {name: '江苏',value: Math.round(Math.random()*2000)},
              {name: '浙江',value: Math.round(Math.random()*2000)},
              {name: '江西',value: Math.round(Math.random()*2000)},
              {name: '湖北',value: Math.round(Math.random()*2000)},
              {name: '广西',value: Math.round(Math.random()*2000)},
              {name: '甘肃',value: Math.round(Math.random()*2000)},
              {name: '山西',value: Math.round(Math.random()*2000)},
              {name: '内蒙古',value: Math.round(Math.random()*2000)},
              {name: '陕西',value: Math.round(Math.random()*2000)},
              {name: '吉林',value: Math.round(Math.random()*2000)},
              {name: '福建',value: Math.round(Math.random()*2000)},
              {name: '贵州',value: Math.round(Math.random()*2000)},
              {name: '广东',value: Math.round(Math.random()*2000)},
              {name: '青海',value: Math.round(Math.random()*2000)},
              {name: '西藏',value: Math.round(Math.random()*2000)},
              {name: '四川',value: Math.round(Math.random()*2000)},
              {name: '宁夏',value: Math.round(Math.random()*2000)},
              {name: '海南',value: Math.round(Math.random()*2000)},
              {name: '台湾',value: Math.round(Math.random()*2000)},
              {name: '香港',value: Math.round(Math.random()*2000)},
              {name: '澳门',value: Math.round(Math.random()*2000)}
            ]
          }]
        });
        // 绘制地图2
        var myChartMap2 = this.$echarts.init(document.getElementById('map2'));
        // 地图上数据
        var myData = [
          {name: '分店1', value: [121.15, 31.89, 90]},
          {name: '分店2', value: [109.781327, 39.608266, 120]},
          {name: '分店3', value: [120.38, 37.35, 142]},
          {name: '分店4', value: [122.207216, 29.985295, 123]},
          {name:'分店5',value:[110.245672,30.7787677,566]}
        ]

        myChartMap2.setOption({

          // 新建一个地理坐标系 geo ，
          geo: {
            map: 'china',//地图类型为中国地图
            itemStyle:{ // 定义样式
              normal:{       // 普通状态下的样式
                areaColor:'#6699CC',
                borderColor: '#fff',
              },
              emphasis: {         // 高亮状态下的样式
                areaColor: '#e9fbf1'
              }
            }

          },
          // hover显示目标数据
          tooltip : {
            trigger: 'item',
            // tooltip的trigger的值可以有'item'、'axis'。
            //'item':数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。
            //'axis':坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用
            textStyle:{
              align:'left'
            },
          },
          // 图表背景色
          backgroundColor: '#404a59',  
          // 标志颜色
          color:'red',
          // 新建散点图series
          series:[{
            name:'',//series名称
            type:'scatter',//为散点类型
            coordinateSystem: 'geo',// series坐标系类型
            data:myData,
            symbol:'pin',
            symbolSize:[20,20]
          }],

          // 添加视觉映射组件
          visualMap: {
            type: 'continuous', // 连续型
            min: 0,           // 值域最小值，必须参数
            max: 600,     // 值域最大值，必须参数
            calculable: true, // 是否启用值域漫游
            inRange: {
              color: ['red']
               // 指定数值从低到高时的颜色变化
            },
            textStyle: {
              color: '#fff' // 值域控件的文本颜色
            }
          }
        })
      },
    },
    mounted(){
      this.initEchart()
    },
  }
</script>
<style scoped>
  #helloworld{
    width: 100%;
  }
  .wrapper{
    width: 76.05%;
    margin:0 auto;
    /*background: #000;*/
  }
  #zhuxingtu{
    width: 800px;
    height:400px;
    float:left;
  }
  #zhuxingtu2{
    width: 800px;
    height:400px;
    margin-left: 10px;
    float:left;
  }
  #shanxingtu{
    width: 800px;
    height:400px;
    margin-top:10px;
    float: left;
  }
  #huanxingtu{
    width: 800px;
    height:400px;
    margin-top:10px;
    float: left;
    margin-left: 10px;
  }
  #map{
    width: 800px;
    height:400px;
    margin-top:10px;
    float: left;
  }
  #map2{
    width: 100%;
    height:800px;
    margin-top:10px;
    float: left;
  }
</style>








