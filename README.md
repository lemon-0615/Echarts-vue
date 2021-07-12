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
效果图![商家销售统计](https://github.com/lemon-0615/Echarts-vue/blob/main/%E6%95%88%E6%9E%9C%E5%9B%BE/%E5%95%86%E5%AE%B6%E9%94%80%E9%87%8F%E7%BB%9F%E8%AE%A1.png)
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
效果图![销量趋势](https://github.com/lemon-0615/Echarts-vue/blob/main/%E6%95%88%E6%9E%9C%E5%9B%BE/%E9%94%80%E9%87%8F%E8%B6%8B%E5%8A%BF%E5%9B%BE.png)
### 图表基本功能的实现
 * 数据的获取:通过函数getData发送ajax请求异步获取数据
   ```
      async getData () {
        // 获取服务器的数据, 对this.allData进行赋值之后, 调用updateChart方法更新图表
        const { data: ret } = await this.$http.get('trend')
        this.allData = ret
        this.updateChart()
     }
   ```
* 数据的处理
     ```
        updateChart () {
          // x轴的数据
          const timeArrs = this.allData.common.month
          // y轴的数据, 暂时先取出map这个节点的数据
          // map代表地区销量趋势
          // seller代表商家销量趋势
          // commodity代表商品销量趋势
          const valueArrs = this.allData.map.data
          // 图表数据, 一个图表中显示5条折线图
          const seriesArr = valueArrs.map((item, index) => {
             return {
                type: 'line', // 折线图
                name: item.name,
                data: item.data,
             }
          })
          const dataOption = {
            xAxis: {
              data: timeArrs
            },
          legend: {
             data: legendArr
            },
          series: seriesArr
             }
            this.chartInstance.setOption(dataOption)
          }
     ```
* 初始化配置
     ```
       const initOption = {
        xAxis: {
          type: 'category',
          boundaryGap: false
        },
       yAxis: {
          type: 'value'
          }
        }
     ```
* 堆叠图效果-要实现堆叠图的效果, series下的每个对象都需要配置上相同的stack属性
### UI 效果的调整
* 主题的使用
* 区域面积的设置-区域面积只需要给series的每一个对象增加一个 areaStyle 即可
* 颜色渐变的设置-颜色渐变可以通过 LinearGradient 进行设置, 颜色渐变的方向从上往下
### 根据标题切换图表
* 布局的实现-增加类样式为 title 的容器
* 数据动态渲染v-for遍历
    ```
       <!-- 销量趋势图表 -->
      <template>
       <div class='com-container'>
        <div class="title">
         <span>{{ title }}</span>
         <span class="iconfont title-icon">&#xe6eb;</span>
         <div class="select-con">
            <div class="select-item" v-for="item in selectTypes" :key="item.key">
              {{ item.text }}
            </div>
         </div>
        </div>
      <div class='com-chart' ref='trend_ref'></div>
      </div>
      </template>
    ```
* 使用计算属性 title 控制标题的内容和标题的可选择项（过度掉当前选中的类别）
     ```
         <script>
         export default {
           data () {
             return {
                chartInstance: null,
                allData: null,
                dataType: 'map' // 这项数据代表目前选择的数据类型, 可选值有map seller
           commodity
         }
        },
        computed: {
           selectTypes () {
              if (!this.allData || ! this.allData.type) {
                return []
          } else {
              return this.allData.type.filter(item => {
                return item.key !== this.dataType
             })
            }
          },
        title () {
          if (!this.allData) {
            return ''
        } else {
          return this.allData[this.dataType].title
           }
          }
         },
      ```
* 点击三角控制显示隐藏-增加一项变量控制可选容器的显示与隐藏，showChoice: false来控制可选面板的显示或者隐藏
* 使用指令 v-if 和点击事件的监听
     ```
      <span class="iconfont title-icon" @click="showChoice =!showChoice">&#xe6eb;</span>
      <div class="select-con" v-if="showChoice">
    ```
* 点击可选条目的控制
    ```
      handleSelect (key) {
        this.dataType = key
        this.updateChart()
        this.showChoice = false
       }
    ```
## 商家地图分布
效果图![销量趋势](https://github.com/lemon-0615/Echarts-vue/blob/main/%E6%95%88%E6%9E%9C%E5%9B%BE/%E5%95%86%E5%AE%B6%E5%88%86%E5%B8%83.png)
### 显示地图
* 获取中国地图矢量数据
* 注册地图数据到 全局echarts对象 中
* 配置 geo
     ```
      <script>
       // 获取的是Vue环境之下的数据, 而不是我们后台的数据
       import axios from 'axios'
       export default {
        ......
        methods: {
          async initChart () {
             this.chartInstance = this.$echarts.init(this.$refs.map_ref)
             const { data: mapData } = await axios.get('http://127.0.0.1:8999/static/map/china.json')
             this.$echarts.registerMap('china', mapData)
             const initOption = {
             geo: {
                 type: 'map',
                 map: 'china'
                 }
               }
               this.chartInstance.setOption(initOption)
             },
      ```
### 显示散点图
 * 获取散点数据
     ```
        async getScatterData () {
          // 获取服务器的数据, 对this.allData进行赋值之后, 调用updateChart方法更新图表
          const { data: ret} = await this.$http.get('map')
          this.allData = ret
          this.updateChart()
       }
     ```
* 处理数据并且更新图表
    ```
      updateChart () {
         // 处理图表需要的数据
          // 图例数据
        const legendData = this.allData.map(item => {
            return item.name
     })
         // 散点数据
       const seriesArr = this.allData.map(item => {
          return {
              type: 'effectScatter',
              coordinateSystem: 'geo',
              name: item.name,
              data: item.children
            }
          })
      const dataOption = {
         legend: {
            data: legendData
          },
            series: seriesArr
         }
         this.chartInstance.setOption(dataOption)
      },
     ```
 ### 地图点击事件
 * 响应图表的点击事件, 并获取点击项相关的数据
 * 将资料中的 map_utils.js 复制到 src/utils/ 目录之下
 * 得到地图所点击项的拼音和地图矢量数据的路径
    ```
       <script>
      // 获取的是Vue环境之下的数据, 而不是我们后台的数据
      import axios from 'axios'
      import { getProvinceMapInfo } from '@/utils/map_utils'
      export default {
       ......
       methods: {
         async initChart () {
         ......
         this.chartInstance.setOption(initOption)
         this.chartInstance.on('click', async arg => {
           // arg.name 就是所点击的省份名称, 是中文
          const provinceInfo = getProvinceMapInfo(arg.name)
          const { data: ret } = await axios.get('http://127.0.0.1:8999' +provinceInfo.path)
          this.$echarts.registerMap(provinceInfo.key, ret)
          this.chartInstance.setOption({
           geo: {
             map: provinceInfo.key
           }
         })
        })
        this.getScatterData()
         }
       }
       }
       </script>
     ```
## 热销商品占比
效果图![销量趋势](https://github.com/lemon-0615/Echarts-vue/blob/main/%E6%95%88%E6%9E%9C%E5%9B%BE/%E5%95%86%E5%AE%B6%E5%88%86%E5%B8%83.png)
### 图表基本功能的实现
* 数据的获取
     ```
       asyncgetData(){
        //获取服务器的数据,对this.allData进行赋值之后,调用updateChart方法更新图表
         const{data:ret}=awaitthis.$http.get('hotproduct')
         this.allData=ret
         this.updateChart()
         },
     ```
 * 数据的处理-增加currentIndex索引代表当前显示的数据索引, 后期通过左右箭头改变currentIndex的值
      ```
        updateChart(){
         //处理图表需要的数据
         //饼图数据
          const seriesData=this.allData[this.currentIndex].children.map(item=>{
           return{
             value:item.value,
             name:item.name
            }
           })
             //图例数据
           const legendData=this.allData[this.currentIndex].children.map(item=>{
             returnitem.name
             })
             constdataOption={legend:{data:legendData},
             series:[
               {
                 data:seriesData
                 }
               ]
             }
             this.chartInstance.setOption(dataOption)
             },
      ```
 ### 切换数据的实现 
 * 布局-在页面上增加箭头的图案，点击事件
      ```
        <!--热销商品图表-->
        <template>
        <div class='com-container'>
           <div class='com-chart'ref='hot_ref'></div>
           <span class="iconfontarr_left" @click="toLeft">&#xe6ef;</span>
           <span class="iconfontarr_right" @click="toRight">&#xe6ed;</span>
           methods:{ toLeft(){
             this.currentIndex--
             if(this.currentIndex<0){
                 this.currentIndex=this.allData.length-1
                 }
               this.updateChart()
               },
             toRight(){
                this.currentIndex++
                if(this.currentIndex>this.allData.length-1){
                   this.currentIndex=0
                   }
                 this.updateChart()
               }
             }
            </div>
         </template>
      ```
 * 分类名称的显示，名称的改变通过增加计算属性catTitle
    ```
      <script>
      export default{
        ......
       computed:{
        catTitle() {
        if(!this.allData) {
          return''
         }
         return this.allData[this.currentIndex].name
         }
        },
      <!--热销商品图表-->
      <template>
           <div class='com-container'>
            ......
            <span class="cat_name">{{catTitle}}</span>
         </div>
        </template>
    ```
 ### UI效果的调整
 * 默认隐藏文字, 高亮显示文字
      ```
         methods: {
           initChart () {
           this.chartInstance = this.$echarts.init(this.$refs.hot_ref, 'chalk')
           const initOption = {
             ......
             series: [
             {
                type: 'pie',
                label: { // 隐藏文字
                show: false
             },
                labelLine: { // 隐藏线
                show: false
             },
             emphasis: {
             label: { // 高亮显示文字
                show: true
                 }
              }
            }
           ]
          }
           this.chartInstance.setOption(initOption)
          },
       ```
 ### 分辨率适配
 * 分辨率适配主要就是在 screenAdapter 方法中进行, 需要获取图表容器的宽度,计算出标题字体大小,将字体的大小赋值给 titleFontSize
     ```
       <script>
      export default {
         data () {
          return {
            titleFontSize: 0
            }
          },
       ......
       screenAdapter () {
         this.titleFontSize = this.$refs.hot_ref.offsetWidth / 100 * 3.6
       }
    ```
* 箭头大小和分类名称:定义计算属性 comStyle
     ```
       computed: {
         ......
         comStyle () {
            return {
              fontSize: this.titleFontSize + 'px'
              }
            }
        },
     ```
 * 将 comStyle 通过 :style 的方式作用到箭头和分类上
    ```
      <template>
       <div class='com-container'>
         <div class='com-chart' ref='hot_ref'></div>
          <span class="iconfont arr_left" @click="toLeft" :style="comStyle">&#xe6ef;</span>
          <span class="iconfont arr_right" @click="toRight :style="comStyle">&#xe6ed;</span>
          <span class="cat_name" :style="comStyle">{{ catTitle }}</span>
        </div>
      </template>
    ```
## 库存销量分析
### 图表基本功能的实现
* 数据的处理, 要显示5个圆环的实现
     ```
        updateChart () {
          // 处理图表需要的数据
          // 5个圆环对应的圆心点
         const centerPointers = [
             ['18%', '40%'],
             ['50%', '40%'],
             ['82%', '40%'],
             ['34%', '75%'],
             ['66%', '75%']
          ]
         // 先显示前5条数据
          const showData = this.allData.slice(0, 5)
          const seriesArr = showData.map((item, index) => {
        return {
          type: 'pie',
          center: centerPointers[index],
          radius: [110, 100],
          data: [
           {
             value: item.sales
           },
           {
            value: item.stock,
           }
          ]
          }
        })
        const dataOption = {
            series: seriesArr
        }
           this.chartInstance.setOption(dataOption)
        },
     ```
### 切换动画
* 增加数据 currentIndex ,标识当前的页数
* 根据 currentIndex 决定展示的数据
     ```
       updateChart () {
        ......
        const start = this.currentIndex * 5
        const end = (this.currentIndex + 1) * 5
        const showData = this.allData.slice(start, end)
        const seriesArr = showData.map((item, index) => {
        ......
     ```
 * 数据获取成功之后启动动画
      ```
          async getData () {
           // 获取服务器的数据, 对this.allData进行赋值之后, 调用updateChart方法更新图表
           const { data: ret } = await this.$http.get('stock')
           this.allData = ret
           this.updateChart()
           this.startInterval()
         },
         ......
         startInterval () {
           if (this.timerId) {
             clearInterval(this.timerId)
           }
         this.timerId = setInterval(() => {
          this.currentIndex++
          if (this.currentIndex > 1) {
            this.currentIndex = 0
          }
            this.updateChart()
         }, 3000)
        }
     ```
* 组件销毁时停止动画
   ```
     destroyed () {
        window.removeEventListener('resize', this.screenAdapter)
        clearInterval(this.timerId)
     },

   ```
* 鼠标事件的处理
    ```
      methods: {
        initChart () {
          ......
          this.chartInstance.on('mouseover', () => {
             clearInterval(this.timerId)
         })
        this.chartInstance.on('mouseout', () => {
            this.startInterval()
        })
       },
    ```
## WebSocket的引入
WebSocket 可以保持着浏览器和客户端之间的长连接， 通过 WebSocket 可以实现数据由后端推送到前端，保证了数据传输的实时性. WebSocket 涉及到前端代码和后端代码的改造
### 后端
* 安装 WebSocket 包npm i ws -S
* 创建 WebSocket 实例对象
    ```
      const WebSocket = require("ws")
      // 创建出WebSocket实例对象
      const wss = new WebSocket.Server({
       port: 9998
      })
    ```
* 监听事件
   ```
    wss.on("connection", client => {
      console.log("有客户端连接...")
      client.on("message", msg => {
         console.log("客户端发送数据过来了")
         // 发送数据给客户端
         client.send('hello socket')
       })
    })
   ```
### 前端的测试代码
  ```
     <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
    </head>
    <body>
       <button id="connect">连接</button>
       <button id="send" disabled="true">发送数据</button> <br>
    从服务器接收的数据如下:<br>
    <span id="content"></span>
    <script>
     var connect = document.querySelector('#connect')
     var send = document.querySelector('#send')
     var content = document.querySelector('#content')
     var ws = null
     connect.onclick = function() {
      ws = new WebSocket('ws://localhost:9998')
      ws.onopen = () => {
       console.log('连接服务器成功')
       send.disabled = false
     }
     ws.onmessage = msg => {
       console.log('从服务器接收到了数据')
       content.innerHTML = msg.data
    }
     ws.onclose = e => {
       console.log('服务器关闭了连接')
       send.disabled = true
      }
     }
     send.onclick = function(){
      ws.send('hello websocket from frontend')
    }
    </script>
    </body>
   </html>

   ```
## 使用WebSocket改造项目
### 后端工程
1. 创建web_socket_service.js
  * 创建Socket对象
  * 监听事件-connection，message
  * 将监听事件的代码放到一个函数中，并将这个函数导出
2. 服务端接受数据字段约定
  * action-代表某项行为，可选值有，getData代表获取图表数据，fullScreen代表产生了全屏事件，thmemChange代表产生了主题切换的事件
  * socketType-代表业务模块类型，代表前端响应函数的标识，可选值有trendData,sellerData,mapData,rankData,hotData,stockData,fullScreen,themeChange
  * chartName-代表图表名称，可选值有trend,seller,map,rank,hot,stock
  * value
4. 服务端发送数据字段约定
   * 接受到action为getData时
    + 取出数据中的chartName字段
    + 拼接json文件的路径
    + 读取该文件的内容
    + 在接受到的数据基础之上，增加data字段，其值就是所读取的文件内容
   * 接受到action不为getData时，原封不动的将从客户端接受到的数据，转发给每一个处于连接状态的客户端
### 前端工程
 1. 创建socket_service.js
   * 定义类SocketService,并定义成单例设计模式定义连接服务器的方法connect
     + 单例模式-这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。
     + 从get Instance中获取SocketService对象，都是同一个对象
       ```
         static instance = null
         static get Instance() {
         if (!this.instance) {
           this.instance = new SocketService()
         }
          return this.instance
          }
       ```
   * 定义连接服务器的方法connect
     + 创建WebSocket对象，对服务器进行连接
       ```
        // 定义连接服务器的方法
       connect() {
         // 连接服务器
        if (!window.WebSocket) return console.log('您的浏览器不支持 WebSocket');
        // this.ws = new WebSocket('ws://localhost:9998')
        // 使用接口地址
        this.ws = new WebSocket('ws://120.53.120.229:9998')
      ```
     + 在main.js中调用此方法
      ```
        // 引入 socket_service
        import SocketService from './utils/socket_service'
        // 对服务端进行 webSocket的连接
        SocketService.Instance.connect()
        Vue.prototype.$socket = SocketService.Instance
      ```
   * 监听事件onopen,onmessage,onclose
   * 存储回调函数,事先将图表模块的方法存储在socket_service.js模块当中，一旦从后端得到数据，调用之前的方法，就可以将数据传递给每一个图表组件
     + callBackMapping={}  存储回调函数
     + registerCallBack(socketType,callBack){}  回调函数注册
     + unRegisterCallBack(socketType){}         回调函数取消
   * 接收数据的处理 onmessage 调用之前存储的回调函数，传递数据
   * 定义发送数据的方法
     ```
       send(data) {
         this.ws.send(JSON.stringify(data))
        }
     ```
   * 挂载SocketService对象到vue的原型对象上
   
 2. 组件的改造
   * create 注册回调函数，指明回调函数的唯一标识sockettype
     ```
        created() {
          // 在组件创建完成之后，进行回调函数的注册
          this.$socket.registerCallBack('trendData', this.getData)
        },
     ```
   * destroyed 取消回调函数
     ```
       destroyed() {
          window.removeEventListener('resize', this.screenAdapter)
          // 销毁注册的事件
          this.$socket.unRegisterCallBack('trendData')
          },
     ```
   * 在原来获取数据的地方，改为发送数据,服务端发送了数据之后，就会调用注册的getData函数，把得到的数据以参数的形式传递给了getData函数，this.allData=ret
       ```
          // websocket 请求数据
          this.$socket.send({
            action: 'getData',
            socketType: 'trendData',
            chartName: 'trend',
            value: '',
         })
        ```
 4. 优化
   * 在WebSocket处于连接状态的时候不可以执行send方法，因为连接需要时间
   * 解决方案，重发数据机制：添加实例属性标识符connected，默认值是false，onopen时设置为true，onclose时设置为false，判断是否连接成功
   * 发送数据时判断connected。true就直接发送，false就延时发送，延时的时长随着尝试的机会而增加，实例属性sendRetryCount
        ```
           // 发送数据的方法
          send(data) {
            if (this.connected) {
              this.sendRetryCount = 0
              // 调用 webSocket 身上的send方法
              // console.log('发送请求：',data);
              this.ws.send(JSON.stringify(data))
            } else {
              // 请求数据尝试的次数,次数变多，等待时间也增长
              this.sendRetryCount++

              setTimeout(() => {
                this.send(data)
              }, this.sendRetryCount * 500);
            }
          }
        ```
  * 断开重连机制，onclose，延时尝试连接服务器，延时的时长随着尝试的机会而增加，实例属性connectRetryCount
  * 如果初始化连接服务端不成功, 或者连接成功了, 后来服务器关闭了, 这两种情况都会触发 onclose 事件,我们需要在这个事件中,进行重连
      ```
        // 连接已关闭  当连接成功后:服务器关闭
       this.ws.onclose = () => {
         this.connectRetryCount++
         this.connected = false
         console.log('连接已关闭');
         setTimeout(() => {
           this.connect() //这时会重新创建WebSocket实例对象
         }, this.connectRetryCount * 500);
       }
      ```
## 细节处理
### 组件合并（先前已做过屏幕适配处理）
1. 创建Home.vue,并配置路由规则
    ```
      const routes = [{
        path: '/',
        redirect: '/home'
      },
      {
        path: '/home',
        component: Home
      },
    ```
2. 创建布局和样式
     * 给每一个图一个框进行存放合适的容器中
3. 注册组件，并将组件置于合适的位置
     * 组件的引入和注册
     * 给图表每一个组件都增加上 ref 属性
       ```
           <div class="screen-body">
            <section class="screen-left">
            <div id="left-top">
               <!-- 销量趋势图表 -->
           <Trend ref="trend"></Trend>
           </div>
           <div id="left-bottom">
             <!-- 商家销售金额图表 -->
             <Seller ref="seller"></Seller>
           </div>
         </section>
          <section class="screen-middle">
         <div id="middle-top">
          <!-- 商家分布图表 -->
           <Map ref="map"></Map>
          </div>
           <div id="middle-bottom">
           <!-- 地区销量排行图表 -->
          <Rank ref="rank"></Rank>
         </div>
          </section>
         <section class="screen-right">
          <div id="right-top">
           <!-- 热销商品占比图表 -->
           <Hot ref="hot"></Hot>
         </div>
         <div id="right-bottom">
         <!-- 库存销量分析图表 -->
           <Stock ref="stock"></Stock>
           </div>
           </section>
         </div>
       ```
4. 调整原有组件样式
  * global.less .com-container
  * Hot.vue 图例大小
  * Stock.vue 圆环的大小
### 全屏切换
1. 布局和样式的调整
      ```
        <div id="left-top">
         <Trend ref="trend"></Trend>
         <div class="resize">
         <span class="iconfont icon-compress-alt"></span>
         </div>
         </div>
       ```
2. 修改各个容器样式, 增加 position 为相对布局relative;
3. 全屏状态数据的定义
     ```
        export default {
          data () {
          return {
          fullScreenStatus: {
          trend: false,
          seller: false,
          map: false,
          rank: false,
          hot: false,
          stock: false
              }
             }
            }
          }
     ```
4. 全屏状态样式的定义
      ```
        .fullscreen {
          position: fixed!important;
          top: 0 !important;
          left: 0 !important;
          width: 100% !important;
          height: 100% !important;
          margin: 0 !important;
          z-index: 100;
          }
       ```
5. 全屏图标的处理，class 值的处理
      ```
        <div id="left-top" :class="[fullScreenStatus.trend ? 'fullscreen' : '']">
         <Trend ref="trend"></Trend>
         <div class="resize">
         <span
         :class="['iconfont', fullScreenStatus.trend ? 'icon-compressalt' : 'icon-expand-alt']"
         @click="changeSize('trend')">
         </span>
         </div>
         </div>
      ```
6. 点击事件的处理
    ```
      export default {
        methods: {
          changeSize (chartName) {
            // 先得到目标状态
            const targetValue = !this.fullScreenStatus[chartName]
            // 将所有的图表设置为非全屏
            Object.keys(this.fullScreenStatus).forEach(item => {
              this.fullScreenStatus[item] = false
          })
          // 将目标图表设置为目标状态
          this.fullScreenStatus[chartName] = targetValue
          this.$nextTick(() => {
            this.$refs[chartName].screenAdapter()
          })
         }
        }
     ```
7. 联动效果-全屏事件的数据发送
   * 点击按钮发送数据
     ```
       export default {
           methods: {
           changeSize (chartName) {
             // 先得到目标状态
             const targetValue = !this.fullScreenStatus[chartName]
             // 将所有的图表设置为非全屏
             // Object.keys(this.fullScreenStatus).forEach(item => {
             // this.fullScreenStatus[item] = false
             // })
             // 将目标图表设置为目标状态
             // this.fullScreenStatus[chartName] = targetValue
             // this.$nextTick(() => {
             // this.$refs[chartName].screenAdapter()
             // })
             this.$socket.send({
                action: 'fullScreen',
                socketType: 'fullScreen',
                chartName: chartName,
                value: targetValue
              })
             }
           }
          }
     ```
 * created 时注册回调函数
       ```
         export default {
          created () {
             this.$socket.registerCallBack('fullScreen', this.recvData)
           },
         }
      ```
 * destroyed 时取消回调函数
      ```
        export default {
          destroyed () {
            this.$socket.unRegisterCallBack('fullScreen')
           },
         }
      ```
  * 得到数据的处理
       ```
         export default {
            methods: {
              recvData (data) {
              // 将所有的图表设置为非全屏
             Object.keys(this.fullScreenStatus).forEach(item => {
                this.fullScreenStatus[item] = false
            })
            // 将目标图表设置为目标状态
            this.fullScreenStatus[data.chartName] = data.value
            // 更新所有图表
            Object.keys(this.fullScreenStatus).forEach(item => {
              this.$nextTick(() => {
                this.$refs[item].screenAdapter()
              })
              })
            }
           }
          }
       ```
  * socket_service.js 代码的修改
      ```
        if (recvData.action === 'getData') {
           const realData = recvData.data // 得到该图表的数据
           this.callBackMapping[socketType].call(this, JSON.parse(realData))
        } else if (action === 'fullScreen') {
           this.callBackMapping[socketType].call(this, recvData)
         }
      ```
### 主题切换
当前主题的数据, 会在多个组件中使用, 因此设置在 VueX 中是最合适的, 增加仓库数据 theme , 并增加一个 mutation 用来修改 theme
  1. 数据的存储 VueX 
      * state theme
      * mutation changeTheme
          ```
              export default new Vuex.Store({
                state: {
                   theme: 'chalk'
              },
              mutations: {
                changeTheme (state) {
                 if (state.theme === 'chalk') {
                   state.theme = 'vintage'
               } else {
                state.theme = 'chalk'
                }
               }
              },
             actions: {
              },
             modules: {
              }
            })
         ```
  2. 点击切换按钮，修改VueX中的theme数据
    * 点击事件的响应
          ```
            <div class="title-right">
               <img src="/static/img/qiehuan_dark.png" class="qiehuan" @click="changeTheme">
             <span class="datetime">2049-01-01 00:00:00</span>
            </div>
          ```
    * 点击事件的处理
         ```
           export default {
            methods: {
              changeTheme () {
               this.$store.commit('changeTheme')
               }
              }
            }

         ```
  3. 各个组件监听theme的变化
    * 映射 store 中的 theme 作为当前组件的计算属性
            ```
              <script>
               import { mapState } from 'vuex'
               export default {
                 computed: {
                   ...mapState(['theme'])
                }
               }
            ```
    * 监听 theme 的变化
            ```
              export default {
               watch: {
                 theme () {
                   this.chartInstance.dispose()
                   this.initChart()
                   this.screenAdapter()
                   this.updateChart()
               }
               }
               }

            ```
  4. 特殊处理-原生HTML主题样式适配
     * 创建 utils/theme_utils.js 文件,定义两个主题下, 需要进行样式切换的样式数据, 并对外导出一个函数, 用于方便的通过主题名称得到对应主题的某些配置项
           ```
             const theme = {
                chalk: {
                   // 背景色
                   backgroundColor: '#161522',
                   // ScreenPage组件中标题的颜色
                   titleColor: '#fff',
                   // 页面左上角logo图标
                   logoSrc: 'logo_dark.png',
                   // 页面顶部头部边框图片
                   headerBorderSrc: 'header_border_dark.png',
                   // 页面右上角切换按钮的图标
                   themeSrc: 'qiehuan_dark.png'
                },
                vintage: {
                  backgroundColor: '#eeeeee',
                  titleColor: '#000',
                  logoSrc: 'logo_light2.png',
                  headerBorderSrc: 'header_border_light.png',
                  themeSrc: 'qiehuan_light.png'
                 }
                }
                export function getThemeValue (arg) {
                  return theme[arg]
                }
            ```
     * Home.vue的调整
            + 映射 VueX 中的 theme 数据作为该组件的计算属性
                    ```
                      import { mapState } from 'vuex'
                         export default {
                           computed: {
                           ...mapState(['theme'])
                         }
                     ```
            + 定义一些控制样式的计算属性
                    ```
                       import { mapState } from 'vuex'
                       import { getThemeValue } from '@/utils/theme_utils'
                       export default {
                         computed: {
                            ...mapState(['theme']),
                       borderSrc () {
                          return '/static/img/' + getThemeValue(this.theme).headerBorderSrc
                        },
                       logoSrc () {
                           return '/static/img/' + getThemeValue(this.theme).logoSrc
                       },
                       themeSrc () {
                          return '/static/img/' + getThemeValue(this.theme).themeSrc
                       },
                       containerStyle () {
                         return {
                            backgroundColor: getThemeValue(this.theme).backgroundColor
                            color: getThemeValue(this.theme).titleColor
                             }
                           }
                          }
                        }
                    ```
     * Trend.vue-修改计算属性 comStyle 和 marginStyle
     
           ```
               import { mapState } from 'vuex'
               import { getThemeValue } from '@/utils/theme_utils'
               export default {
                   computed: {
                      comStyle () {
                    return {
                      fontSize: this.titleFontSize + 'px',
                      color: getThemeValue(this.theme).titleColor
                   }
               },
               marginStyle () {
                   return {
                      marginLeft: this.titleFontSize + 'px',
                      backgroundColor: getThemeValue(this.theme).backgroundColor,
                     color: getThemeValue(this.theme).titleColor
                    }
                  },
                  ...mapState(['theme'])
                 },
               }
           ```
   * Hot.vue-修改计算属性 comStyle
           ```
               import { mapState } from 'vuex'
               import { getThemeValue } from '@/utils/theme_utils'
               export default {
                 computed: {
                    comStyle () {
                      return {
                         fontSize: this.titleFontSize + 'px',
                         color: getThemeValue(this.theme).titleColor
                     }
                   },
                    ...mapState(['theme'])
                    }
                  }
           ```
  5. 联动效果
