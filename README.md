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
         }
       ```
### 雷达图
  1. ECharts最基本的代码结构
  2. 定义各个维度的最大值, 通过radar属性配置，易用性,功能,拍照,跑分,续航, 每个维度的最大值都是100
  3. 准备产品数据, 设置给series下的data
  4. 将type的值设置为radar
### 仪表盘
  1. ECharts最基本的代码结构：引入js文件，DOM容器，初试化对象，设置option
  2. 准备数据, 设置给series下的data
  3. 将type的值设置为gauge
### 图表使用场景
* 柱状图:柱状图描述的是分类数据，呈现的是每一个分类中有多少
* 折线图:折线图常用来分析数据随时间的变化趋势
* 散点图:散点图可以帮助我们推断出不同维度数据之间的相关性
* 饼图:饼图可以很好地帮助用户快速了解不同分类的数据的占比情况

## 前端工程创建
具体的配置项如下：
 * 手动选择特性
 * 集成 Router , Vuex , CSS Pre-processors
 * 选择 Less 作为 CSS 的预处理器(no)
 * 选择 Less 作为 CSS 的预处理器
 * 选择 ESLint 的配置
 * 什么时候进行 Lint 提示
 * 如何存放 Babel , ESLint 等配置文件:In dedicated config files
 * 是否保存以上配置以便下次创建项目时使用
### 在项目根目录下创建 vue.config.js 文件
  在文件中增加代码:
 ```
   // 使用vue-cli创建出来的vue工程, Webpack的配置是被隐藏起来了的
   // 如果想覆盖Webpack中的默认配置,需要在项目的根路径下增加vue.config.js文件
  module.exports = {
    devServer: {
    port: 8999, // 端口号的配置
    open: true // 自动打开浏览器
    }
  }
 ```
### 引入 echarts 包
 * 将资料文件夹中的 static 目录复制到 public 目录之下
 * 在 public/index.html 文件中引入 echarts.min.js 文件
 * 在 src/main.js 文件中挂载，由于在 index.html 中已经通过script标签引入了 echarts.js 文件夹, 故在 window 全局对象中是存在 echarts 全局对象, 将其挂载到 Vue 的原型对象上
  ```
   // 将全局echarts对象挂载到Vue的原型对象上
   Vue.prototype.$echarts = window.echarts
  ```
## 商家销量排行
效果图
### 组件结构设计
在 src/components/ 目录下建立 Seller.vue，这个组件是真实展示图表的组件
  * 给外层div增加类样式 com-container
  * 建立一个显示图表的div元素
  * 给新增的这个div增加类样式 com-chart
在 src/views/ 目录下建立 SellerPage.vue ,这个组件是对应于路由 /seller 而展示的
  * 给外层div元素增加样式 com-page
  * 在 SellerPage 中引入 Seller 组件,并且注册和使用
  * 增加路由规则, 在 src/router/index.js 文件中修改
### 图表Seller.vue基本功能的实现
  * 在mounted生命周期中初始化 echartsInstance 对象
  * 在mounted中获取服务器的数据
  * 将获取到的数据设置到图表上
 ```
   <script>
   export default {
    data () {
      return {
       chartInstance: null, // echarts实例对象
       allData: [] // 服务器获取的所有数据
      }
   },
   mounted () {
     // 由于初始化echarts实例对象需要使用到dom元素,因此必须要放到mounted中, 而不是created
     this.initChart()
     this.getData()
   },
   methods: {
    initChart () {
    this.chartInstance = this.$echarts.init(this.$refs.seller_ref) // 初始化echarts实例对象
   },
   async getData () {
     const { data: res } = await this.$http.get('seller') // 获取数据
     this.allData = res
   // 对allData进行从大到小的排序
    this.allData.sort((a, b) => {
      return a.value - b.value
    })
     this.updateChart()
   },
   updateChart () {
     // 处理数据并且更新界面图表
    const sellerNames = this.allData.map((item) => {
       return item.name
   })
   const sellerValues = this.allData.map((item) => {
      return item.value
   })
   const option = {
    xAxis: {
      type: 'value'
    },
    yAxis: {
      type: 'category',
      data: sellerNames
    },
    series: [
   {
      type: 'bar',
      data: sellerValues
     }
    ]
   }
     this.chartInstance.setOption(option)
       }
     }
   }
   </script>
 ```
 * 拆分配置项option
    * 初始化配置项(和数据无关）
    * 拥有数据之后的配置项
 * 分页动画的实现
   * 数据的处理, 每5个元素显示一页
   * 数据的处理
   ```
       this.totalPage = Math.ceil(this.allData.length / 5)
       const start = (this.curretnPage - 1) * 5
       const end = this.curretnPage * 5
       const showData = this.allData.slice(start, end)
   ```
   * 动画的启动和停止：通过定时器标识，开启定时器刷新效果
   * 鼠标事件的处理 
     ```
      this.chartInstance.on('mouseover', () => {
         this.timerId && clearInterval(this.timerId)
       })
      ```
 ### 分辨率适配
* 对窗口大小变化的事件进行监听
```
 mounted () {
    this.initChart()
    this.getData()
    window.addEventListener('resize', this.screenAdapter)
}
```
* 组件销毁时取消监听
```
 destroyed () {
   clearInterval(this.timerId)
   // 在组件销毁的时候, 需要将监听器取消掉
   window.removeEventListener('resize', this.screenAdapter)
 },
```
* 获取图表容器的宽度计算字体大小
```
  // 当浏览器的大小发生变化的时候, 会调用的方法, 来完成屏幕的适配
  screenAdapter () {
  // console.log(this.$refs.seller_ref.offsetWidth)
  const titleFontSize = this.$refs.seller_ref.offsetWidth / 100 * 3.6
```
 ## 销量趋势分析
