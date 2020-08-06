```html
<template>
  <div :style="{ height: height, width: width }"></div>
</template>
```

```js
<script>
import echarts from "@/utils/echarts";

import resize from "@/components/echarts/mixins/resize";
export default {
  mixins: [resize],
  props: {
    width: {
      type: String,
      default: "100%",
    },
    height: {
      type: String,
      default: "200px",
    },
    chartData: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      chart: null,
    };
  },
  watch: {
    height(val) {
      if (this.chart) {
        this.chart.resize();
      }
    },
    chartData: {
      deep: true,
      handler(val) {
        this.setOptions(val);
      },
    },
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart();
    });
  },
  beforeDestroy() {
    if (!this.chart) {
      return;
    }
    this.chart.dispose();
    this.chart = null;
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, "macarons");
      this.setOptions(this.chartData);
    },
    setOptions({ xData, data1, data2 } = {}) {
      const option = {};
      this.chart.setOption(option);
    },
  },
};
</script>
```

`resize.js`

```js
import { debounce } from "@/utils";

export default {
  data() {
    return {
      $_sidebarElm: null,
    };
  },
  mounted() {
    this.__resizeHandler = debounce(() => {
      if (this.chart) {
        this.chart.resize();
      }
    }, 100);
    window.addEventListener("resize", this.__resizeHandler);

    this.$_sidebarElm = document.getElementsByClassName("sidebar-container")[0];
    this.$_sidebarElm &&
      this.$_sidebarElm.addEventListener(
        "transitionend",
        this.$_sidebarResizeHandler
      );
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.__resizeHandler);

    this.$_sidebarElm &&
      this.$_sidebarElm.removeEventListener(
        "transitionend",
        this.$_sidebarResizeHandler
      );
  },
  methods: {
    // use $_ for mixins properties
    // https://vuejs.org/v2/style-guide/index.html#Private-property-names-essential
    $_sidebarResizeHandler(e) {
      if (e.propertyName === "width") {
        this.__resizeHandler();
      }
    },
  },
};
```
