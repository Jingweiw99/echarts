<template>
  <router-view></router-view>
</template>

<script>
import * as echarts from 'echarts'
import { provide } from 'vue'
import axios from 'axios'

// 设置baseURL
axios.defaults.baseURL = 'http://121.40.153.45:6666'
export default{
  setup(){
    provide('echarts',echarts)
    provide('axios',axios)
  }
}

</script>


<style lang="less">
body{
  background: url("~@/assets/bg.jpg") top center no-repeat;
}
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>

