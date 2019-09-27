# echarts：折线图配置

## 一、 导入echarts

### npm 安装echarts

`npm install echarts --save`详见：[在 webpack 中使用 echarts](http://echarts.baidu.com/tutorial.html#%E5%9C%A8%20webpack%20%E4%B8%AD%E4%BD%BF%E7%94%A8%20ECharts)

### 引入 echarts

通过 npm 上安装的 ECharts 和 zrender 会放在`node_modules`目录下。可以直接在项目代码中 `require('echarts')` 得到 ECharts。

#### 全局引入echarts

* 在main.js文件中引入echarts，然后将echarts拓展到vue对象上。

  ~~~javascript
  import echarts from 'echarts';
  import Vue from 'Vue';
  
  Vue.prototype.$echarts = echarts;
  ~~~

  ~~~javascript
  methods: {
      initEcharts() {
        const option = {
          // echarts配置项
        };
        const myChart = this.$echart.init(this.$refs.lineChart);
        myChart.setOption(option);
      },
  }
  ~~~

#### 单个文件引入echarts

* 在需要引入的文件中直接引入echarts对象。

  ~~~ javascript
  import echarts from 'echarts';
  <script>
    methods: {
      initEcharts() {
        const option = {
          // echarts配置项
        };
        const myChart = echart.init(this.$refs.lineChart); // 获取echart实例
        myChart.setOption(option); // 将配置注入实例
      },
    }
  </script>
  ~~~

### echarts配置项

~~~
option: {
  title: { // 标题配置
    text: '未来一周气温变化', // 大标题
    subtext: '纯属虚构', // 小标题
  },
  tooltip: { // 提示框组件
    trigger: 'axis', // item-数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。axis-坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用。none-什么都不触发。
  },
  legend: { // 图例名(与下面的name保持统一)
    data: ['最高气温', '最低气温'],
  },
  toolbox: {
    show: true, // 是否显示工具栏组件
    orient: 'horizontal', // 工具栏 icon 的布局朝向。horizontal/vertical
    feature: { // 各工具配置项，自定义工具特定以my开头
      dataZoom: {}, // 数据区域缩放。目前只支持直角坐标系的缩放。
      dataView: { readOnly: false }, // 数据视图工具，可以展现当前图表所用的数据，编辑后可以动态更新。
      magicType: { type: ['line', 'bar'] }, // 动态类型切换 
      restore: {}, // 配置项还原
      saveAsImage: {}, // 保存为图片
    },
  },
  xAxis: { // x轴配置
    type: 'category', // 轴类型
    boundaryGap: false, 
    data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],
  },
  yAxis: { // Y轴配置
    type: 'value',
    name: '(°C)', // 坐标轴名称
    nameTextStyle: { // 名称样式
      padding: [0, 20, 0, 0],
    },
    axisLabel: {
      formatter: '{value}',
    },
  },
  dataZoom: [ // 区域缩放组件
    {
	  type: 'inside', // 鼠标缩放功能
    },{
	  type: 'slider', // 滑块配置
    }
  ],
  series: [ // 数据配置
    {
      name: '最高气温',
      type: 'line',
      data: [11, 11, 15, 13, 12, 13, 10],
      symbol: '', // 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow', 'none';标记类型
      itemStyle: {}, // 标记样式 折线颜色默认与标记颜色相同
      lineStyle: {}, // 折线样式
      emphasis: { // 高亮时的样式
          label: {}, // 标签配置
          itemStyle: {}, // 标记样式
      },
      markPoint: { // 辅助标注
        data: [
          { type: 'max', name: '最大值' },
          { type: 'min', name: '最小值' },
        ],
      },
      markLine: { // 辅助线
        data: [
          { type: 'average', name: '平均值' },
        ],
      },
    },
    {
      name: '最低气温',
      type: 'line',
      data: [1, -2, 2, 5, 3, 2, 0],
      markPoint: {
        data: [
          {
            name: '周最低',
            value: -2,
            xAxis: 1,
            yAxis: -1.5,
          },
        ],
      },
      markLine: {
        data: [
          { type: 'average', name: '平均值' },
        ],
      },
    },
  ],
},
~~~

![1544766568801](C:\Users\my\AppData\Roaming\Typora\typora-user-images\1544766568801.png)

### 图表大小自适应

```javascript
initLineEcharts() {
  const myChart = Echart.init(this.$refs.lineChart);
  myChart.setOption(this.option);
  window.onresize = () => { // 绑定到Windows对象上，随窗口大小改变而改变
    myChart.resize();
  };
},
```

