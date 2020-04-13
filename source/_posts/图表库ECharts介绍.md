---
title: 图表库ECharts介绍
date: 2017-8-26 19:33
tags: ECharts
categories: 前端
summary_img: http://p4z3kz4fz.bkt.clouddn.com/snipaste_20180307_114203.png
---
## 简介

​	ECharts是百度公司出品的一款非常强大的数据可视化工具，[补充说明，目前已经推出微信小程序](https://github.com/ecomfe/echarts-for-weixin),那么就让我们一起来了解如何使用入门吧。

​	ECharts，一个纯 Javascript 的图表库，可以流畅的运行在 PC 和移动设备上，兼容当前绝大部分浏览器（IE8/9/10/11，Chrome，Firefox，Safari等），提供直观，生动，可交互，可高度个性化定制的数据可视化图表。ECharts 提供了常规的折线图，柱状图，散点图，饼图，K线图，用于统计的盒形图，用于地理数据可视化的地图。

<!--more-->

## 官网

github: https://github.com/ecomfe/echarts

ECharts官网: http://echarts.baidu.com/

star：23k+

## 步骤

#### 引入js文件

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <!-- 引入 ECharts 文件 -->
    <script src="echarts.min.js"></script>
</head>
</html>
```

#### 准备一个dom容器

```HTML
<div id="main" style="width: 600px;height:400px;"></div>
```

#### 初始化一个实例

```javascript
<script type="text/javascript">
        // 基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));
</script>
```

#### 设置图表的配置项和数据

```javascript
// 指定图表的配置项和数据
        var option = {
            title: {
                text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
                data:['销量']
            },
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        };
```

#### 最后，显示图表

```javascript
myChart.setOption(option);
```

## API

#### echarts

- echarts.init(dom,theme,opts)   实例一个图表对象
  - dom   实例容器，一般是一个具有高宽的`div`元素。
  - theme 应用的主题。
  - opts  可选参数
    - width  可显式指定实例宽度，单位为像素。如果传入值为 `null`/`undefined`/`auto`，则表示自动取 `dom`（实例容器）的宽度。
    - height  可显式指定实例高度，单位为像素。如果传入值为 `null`/`undefined`/`'auto'`，则表示自动取 `dom`（实例容器）的高度。
    - renderer  渲染器
- echart.connect(group)    多个图表实例实现联动
  - group  图表实例的 id，或者图表实例的数组。
- echarts.getInstanceByDom  获取dom容器上的实例

## 图表配置项

- **title**  标题组件

  - text    `string` 主标题文本
  - link    `string` 主标题文本超链接
  - target    `string`  超链接打开方式
    - self   当前窗口
    - blank   新窗口
  - subtext    `string`  副标题文本
  - left/right/top/bottom   距离容器的距离

- **legend**   图例组件

  - type   图例类型
    - plain    普通图例
    - scroll  可滚动翻页的图例
  - orient    图例列表的布局朝向
    - horizontal
    - vertical
  - left/right/top/bottom
  - data
  - formatter    格式化图例文本

- **xAxis**  /  **yAxis**

  - name     `string`  坐标轴名称
  - type    `string`  坐标轴类型
    - value   竖直轴 适用于连续数据
    - category 类目轴，适用于离散的类目数据，为这个类型的时候必须使用data来设置类目数据
    - time   时间轴  适用于连续的时序数据
    - log   对数轴 适用于对数数据
  - min   坐标轴刻度最小值
  - max    坐标轴刻度最大值
  - inverse    是否反向坐标轴  默认false    ECharts3新添加

- **tooltip**  提示框组件

  - trigger    触发类型
    - item   主要在散点图，饼图等无类目轴的图表中使用
    - axis    坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用
    - none   什么都不触发
  - triggerOn    提示框触发条件
    - mouseover
    - click
    - mouseover|click
    - none
  - confine  是否将提示框限制在图标都区域内  default:false

- **series**   系列列表

  - type 图表类型

    - line    折线图				bar          柱状图/条形图

      pie     饼图				scatter    散点图

      map   地图				...

  - name  系列名称  用于tooltip的显示

  - data    系列中的数据内容数组。数组项通常为具体的数据项。

  - markPoint  图标标记

  - markLine    图表标记线

## 案例(浏览器使用率)：

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script src="js/echarts.common.min.js"></script>
  <style>
    #main {
      width: 600px;
      height: 400px;
      margin: 100px auto;
    }
  </style>
</head>
<body>

<div id="main"></div>

<script>
  var chart = echarts.init(document.querySelector("#main"));

  var option = {
    title: {
      text: "各浏览器使用量",
      subtext: "纯属虚构",
      left: "center"
    },
    tooltip: {
      trigger: "item",
      formatter: "{a} <br/>{b} : {c} ({d}%)"
    },
//    legend: {
//      orient: "vertical",
//      left: "left",
//      data: ["张三","王二","找钱","孙俪","周哈","李四"]
//    },
    legend: {
      orient: 'vertical',
      left: 'left',
      data: ['Chrome', 'Firefox', 'IE', 'Opera', 'Safari']
    },
    series: [
      {
        name: "浏览器使用比例",
        type: "pie",
        radius: "50%", //圆形半径 支持百分比 百分比的时候 是相对一容器宽高较小的那项的一半
        center: ["50%", "50%"],
        data: [
          {value: 50000, name: "Chrome"},
          {value: 35000, name: "Firefox"},
          {value: 10000, name: "IE"},
          {value: 15000, name: "Opera"},
          {value: 20000, name: "Safari"}
        ]
      }
    ]
  }
  chart.setOption(option);
</script>
</body>
</html>
```

效果图：

​					<img src="http://p4z3kz4fz.bkt.clouddn.com/snipaste_20180307_115013.png">