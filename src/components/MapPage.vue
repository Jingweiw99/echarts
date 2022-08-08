<template>
    <div class="map" id="map">
        map
    </div>
</template>

<script>
import axios from 'axios'
import { onMounted, reactive, inject } from "vue";
export default {
  setup() {
    let $echarts = inject("echarts");
    let mapData = reactive({});
    async function getState() {
      mapData = await axios.get("http://localhost:8080/map/china.json");
      
    }

    onMounted(() => {
      getState().then(() => {
        // console.log("map", mapData.data);
        $echarts.registerMap("china", mapData.data);
        let myChart = $echarts.init(document.getElementById("map"));
        myChart.setOption({
          geo: {
            map: "china",
            itemStyle: {
              areaColor: "#0099ff",
              borderColor: "#00ffff",
              shadowColor: "rgba(230,130,70,0.5)",
              shadowBlur: 30,
              emphasis: {
                focus: "self",
              },
            },
          },

       
        });
      });
    });
    return {
      getState,
      mapData,
    };
  },
};
</script>


<style lang="less" scoped>
.map {
    width: 100%;
    height: 100%;
}
</style>