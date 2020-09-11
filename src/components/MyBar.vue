<!-- 柱状图 -->
<template>
  <div
    :id="id"
    :class="className"
    :series="seriesData"
    :style="{ height: height, width: width }"
  ></div>
</template>

<script>
import echarts from "echarts";
// const animationDuration = 6000;
export default {
  props: {
    id: {
      type: String,
      default: "chart"
    },
    className: {
      type: String,
      default: "chart"
    },
    seriesData: {
      type: Array,
      default() {
        return [];
      }
    },
    width: {
      type: String,
      default: "100%"
    },
    height: {
      type: String,
      default: "300px"
    }
  },
  data() {
    return {
      chart: null,
      options: {
        tooltip: {
          trigger: "axis",
          axisPointer: {
            // 坐标轴指示器，坐标轴触发有效
            type: "shadow" // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        grid: {
          top: 10,
          left: "2%",
          right: "2%",
          bottom: "3%",
          containLabel: true
        },
        xAxis: [
          {
            type: "category",
            data: ["html", "css", "javascript", "vue"],
            axisTick: {
              alignWithLabel: true
            }
          }
        ],
        yAxis: [
          {
            type: "value",
            axisTick: {
              show: false
            }
          }
        ],
        series: [
          {
            data: [],
            type: "bar"
          }
        ]
      }
    };
  },
  watch: {
    seriesData: {
      handler(newVal, oldVal) {
        if (this.chart) {
          if (newVal) {
            this.options.series[0].data = newVal;
          } else {
            this.options.series[0].data = oldVal;
          }
          this.chart.setOption(this.options);
        } else {
          this.initChart();
        }
      },
      deep: true
    }
  },
  //生命周期 - 创建完成（访问当前this实例）
  mounted() {
    this.$nextTick(() => {
      this.initChart();
    });
  },
  methods: {
    initChart() {
      this.chart = echarts.init(document.getElementById(this.id));
      this.chart.setOption(this.options, true);
    }
  }
};
</script>
<style lang="scss" scoped>
/* @import url(); 引入css类 */
</style>
