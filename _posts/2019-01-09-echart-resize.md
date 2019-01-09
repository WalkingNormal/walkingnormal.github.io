---
title: Echart 自适应
date: 2019-01-09 10:16
categories:
tags:
---

图表是放在一个 `contenter` 中，页面中只有一个 `Echart` 实例。因为是 `ajax` 调用图表数据， 绘制方法是单独调用的。

只要在代码中增加 `window.onresize = myChart.resize;` 就可以了。

```javascript
function showChart(xData, sData){
// 基于准备好的dom，初始化echarts实例
var myChart = echarts.init(document.getElementById('main'),'light');

// 指定图表的配置项和数据
var option = {
    tooltip: {
        trigger: 'axis'
    },
    xAxis: {
        type: 'category',
        boundaryGap: false,
        data: xData
    },
    yAxis: {
        type: 'value'
    },
    series: [{
        data: sData,
        type: 'line',
        smooth: true,
        areaStyle: {}
    }]
};

// 使用刚指定的配置项和数据显示图表。
myChart.setOption(option);
window.onresize = myChart.resize; // 放在这里
}
```
