<template>
  <div class="echarts-box">
    <div id="myEcharts" :style="{ width: '125%', height: '100%' }"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted } from 'vue';
import * as echarts from 'echarts';

export default defineComponent({
  setup() {
    onMounted(() => {
      type EChartsOption = echarts.EChartsOption;
      var chartDom = document.getElementById('myEcharts')!;

      // 获取自适应的高度和宽度
      var resizeMyChartContainer = function () {
        // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
        chartDom.style.height = window.innerHeight * 0.65 + 'px';
        // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
        chartDom.style.width = '100%';

      };

      var myChart = echarts.init(chartDom);
      var option: EChartsOption;

      const x_data = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
      const channel = ['1', '2', '3', '4', '5', '6', '7'];

      const data_ = [820, 932, 901, 934, 1290, 1330, 1320];

      const title: echarts.TitleComponentOption[] = [];
      const xAxis: echarts.XAXisComponentOption[] = [];
      const yAxis: echarts.YAXisComponentOption[] = [];
      const grid: echarts.GridComponentOption[] = [];

      const series: echarts.LineSeriesOption[] = [];

      channel.forEach(function (day, idx) {
        title.push({
          textBaseline: 'middle',
          // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
          top: ((idx + 0.9) * 100) / 0.7 + 'px',
          left: '1%',
          text: day,
        });

        xAxis.push({
          type: 'category',
          boundaryGap: false,
          data: x_data,
          gridIndex: idx,
        });

        yAxis.push({
          type: 'value',
          gridIndex: idx,
        });

        grid.push({
          height: '25%',
          // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
          top: (idx * 320) / 2 + 35 + 'px',
        });

        series.push({
          data: data_,
          type: 'line',
          smooth: true,
          // showSymbol: false,
          xAxisIndex: idx,
          yAxisIndex: idx,
        });
      });

      option = {
        title: title,
        xAxis: xAxis,
        yAxis: yAxis,
        grid: grid,
        series: series,
        tooltip: {
          trigger: 'axis',
        },
        toolbox: {
          right: 10,
          feature: {
            dataZoom: {
              yAxisIndex: 'none',
            },
            restore: {},
            saveAsImage: {},
          },
        },
      };
      option && myChart.setOption(option);

    //   自适应高和宽
      window.onresize = function () {
        resizeMyChartContainer();
        myChart.resize();
      };
    });
  },
});
</script>

<style scoped>
#echarts-box:first-child {
  height: '1000px';
}
</style>
