echarts 的完整包太大了，但是在项目中，其实很多都是用不上的，所以按需引入是很有必要的

- 我的解决方案是定义一个文件，里面引入项目中使用到的所有包，然后使用到的组件中进行
- [echarts可选引入包参考链接](https://github.com/apache/incubator-echarts/blob/master/index.js)

```js
import echarts from "echarts/lib/echarts";

import "echarts/lib/chart/bar";
import "echarts/lib/chart/line";
import "echarts/lib/chart/pie";
import "echarts/lib/component/legend";
import "echarts/lib/component/title";
import "echarts/lib/component/tooltip";
import "echarts/lib/component/grid";
// import 'echarts/theme/macarons' // echarts theme
import installTheme from "./echarts-theme";
installTheme(echarts);

export default echarts;
```

- 这里的主题使用了自定义的主题(基本上是删除了没用上图形的颜色样式)，因为我发现使用 echarts 自带的主题会按需引入失败(因为定义了所有的图形样式形状)
- [主题参考链接](https://echarts.apache.org/zh/download-theme.html)

```js
export default function installTheme(echarts) {
  var colorPalette = [
    "#2ec7c9",
    "#b6a2de",
    "#5ab1ef",
    "#ffb980",
    "#d87a80",
    "#8d98b3",
    "#e5cf0d",
    "#97b552",
    "#95706d",
    "#dc69aa",
    "#07a2a4",
    "#9a7fd1",
    "#588dd5",
    "#f5994e",
    "#c05050",
    "#59678c",
    "#c9ab00",
    "#7eb00a",
    "#6f5553",
    "#c14089",
  ];

  var theme = {
    color: colorPalette,

    title: {
      textStyle: {
        fontWeight: "normal",
        color: "#008acd",
      },
    },

    tooltip: {
      backgroundColor: "rgba(50,50,50,0.5)",
      axisPointer: {
        type: "line",
        lineStyle: {
          color: "#008acd",
        },
        crossStyle: {
          color: "#008acd",
        },
        shadowStyle: {
          color: "rgba(200,200,200,0.2)",
        },
      },
    },

    grid: {
      borderColor: "#eee",
    },

    line: {
      smooth: true,
      symbol: "emptyCircle",
      symbolSize: 3,
    },
  };

  echarts.registerTheme("macarons", theme);
}
```
