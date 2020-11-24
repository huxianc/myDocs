<!--
 * @Description:
 * @Author: huxianc
 * @Date: 2020-11-05 15:15:51
 * @LastEditors: huxianc
 * @LastEditTime: 2020-11-05 15:45:54
-->

1. 需要放到 public 文件夹下，不然放到 asset 下回经过 webpack 处理后 konva 读取到了显示不出来
2. 异步加载的图片如果需要作为底图，之后绘制的图形要在 onload 中绘制后在绘制
