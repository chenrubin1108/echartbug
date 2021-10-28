<template>
  <div>
    <div @click="clickEvent">点击请求接口动态改变x轴数据</div>
    <div style="width: 600px;height:400px;" id="myChartdom"></div>
  </div>
</template>
<script>
import {
  defineComponent,
  ref,
  getCurrentInstance,
  onMounted,
  nextTick,
} from "vue";
import * as echarts from "echarts";
export default defineComponent({
  setup() {
    // 初始化
    let EchartDataNameList = ref([]);
    let initEchart = () => {
      let myChartdom = echarts.init(document.getElementById("myChartdom"));
      myChartdom.on("click", function (params) {
        if (params.componentType == "xAxis") {
          console.log("xAxis");
          return;
          // alert("单击了"+params.value+"x轴标签");
        }
        
      });
      myChartdom.setOption({
        title: {
          text: "人数",
        },
        xAxis: {
          // 宽度
          type: "category",
          data:["1","2","3"],
          // data: EchartDataNameList.value,

          silent: false,
          triggerEvent: true,
          axisLabel: {
            rotate: 52,
            fontWeight: "bolder",
            clickable: true,
          },
          axisLine: {
            lineStyle: {
              color: "#5470C6",
              fontWeight: "bolder",
            },
          },
        },
        yAxis: {},
        dataZoom: {
          realtime:true,
          height: 10,
          start: 40,
          end: 65,
        },
        series: [
          {
            name: "标签内容",
            type: "bar",
            barWidth: 20,
            data: [
              5, 20, 50, 10, 10, 20, 2, 50, 10, 10, 20, 2, 50, 10, 10, 20, 2,
              50, 10, 10, 20, 2, 50, 10, 10, 20, 2, 50, 10, 10, 20, 2,
            ],
            label: {
              show: true, // 开启显示
              // rotate: 70, // 旋转70度
              position: "inside", // 数值
              // distance: 20, // 距离图形元素的距离。当 position 为字符描述值（如 'top'、'insideRight'）时候有效。
              verticalAlign: "middle",
              textStyle: {
                // 数值样式
                color: "white",
                fontSize: 12,
              },
            },
          },
        ],
      });
      window.onresize = function () {
        myChartdom.resize();
      };
    };

    let clickEvent = () => {
      // 像这样请求数据
      // proxy.$axios
      // .get(
      //   url
      //   )
      // )
      // .then(async (res) => {
      //   if (res) {
        // EchartDataNameList ["公司名称","公司名称2"]
      //   EchartDataNameList.value =res.map((res) => res.name)
      //   }
      //   await nextTick();
      // });
    };
    onMounted(() => {
      initEchart();
    
    });
    return { initEchart, clickEvent };
  },
});
</script>