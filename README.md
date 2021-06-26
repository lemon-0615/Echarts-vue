# Echarts-vue
写在前面
1. 数据可视化的概念和作用
  * 将数据以图表的形式呈现
  * 更有效的传达数据中的信息
2. 常见的可视化工具
  * 报表类
  * BI类
  * 编程类
## 电商平台数据可视化实时监控系统-Echarts-vue项目
* 为电商平台数据可视化实时监控
* 可以保证实时获取数据进行分析
* 支持大屏展示，自适应分辨率
* 支持联动效果，一端操作，多端联动展示
## 技术选型
 * ECharts-完成图表的绘制
 * vue,vue router, vuex
 * webpack
 * axios-前后端数据交互
 * websocket 前后端数据推送（开始用axios实现前端向后端的数据获取，在项目后期进行websocket改造，将数据的交互方式由后端向前端推送）
## Echarts的基本使用
### Echarts的介绍
 * ECharts是一个使用JavaScript实现的开源可视化库，兼容性强，底层依赖矢量图形库ZRender，提供直观，交互丰富，可高度个性化定制的数据可视化图表。
 * 开源免费，功能丰富，社区活跃
 * 多种数据格式的支持：key-value数据格式，二维表，TypendArray
 * 流数据的支持，移动端优化，跨平台使用，绚丽的特效，三维可视化
###  5分钟上手ECharts
  * 引入echarts.js文件
  * 准备一个呈现图表的盒子
  * 初始化echarts实例对象
  * 准备配置项
     * 相关配置讲解
     * xAxis:直角坐标系中的×轴yAxis:直角坐标系中的y轴
     * series:系列列表。每个系列通过type决定自己的图表类型
  * 将配置项设置给echarts实例对象
注：toolboxtoolbox: ECharts提供的工具栏
* 内置有导出图片，数据视图，动态类型切换，数据区域缩放，重置五个工具
* 显示工具栏按钮feature：saveAsIamge,dataView,restore,dataZoom,magicType
### 矢量地图的实现步骤
* ECharts最基本的代码结构: 引入js文件,DOM容器,初始化对象，设置option
* 准备中国的矢量地图json文件,放到json/map/的目录下china.json
* 使用Ajax获取china.json
   $.get('json/map/china.json' , function (chinajson) 0)
* 在回调函数中往echarts全局对象注册地图的json数据：echarts.registerMap('chinaMap', chinajson);
* 在geo下设置：type:'map'map: 'chinaMap'
     ```
     <script>
         var mCharts=echarts.init(document.querySelector("div"))
         $.get('json/china.json',function(ret){
             echarts.registerMap('chinaMap',ret)
         var option={
             geo:{
                 type:'map',
                 map:'chinaMap',
                 roam:true
             }
             }
         mCharts.setOption(option)
         })

     </script>
     ```
* 常见效果:地图和散点图结合
 1. 给series下增加新的对象
 2. 准备好散点数据,设置给新对象的data
 3. 配置新对象的type-type:effectScatter
 4. 让散点图使用地图坐标系统coordinateSystem: 'geo'，
 5. 让涟漪的效果更加明显
    ```
     rippleEffect: {
     scale: 10
     )
   ```
  
