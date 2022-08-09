<template>
    <div>
        <h2>库存统计</h2>
        <div class="chart" id="myEchartsThree">

        </div>
    </div>
</template>

<script>
import { inject, onMounted, reactive } from 'vue'

export default {
    setup() {
        let $echarts = inject("echarts")
        let $http = inject('axios')
        let data = reactive({})
        async function getState() {
            data = await $http({ url: "/three/data" })
        }
        onMounted(() => {

            getState().then((res) => {

                // console.log(res, 'res')
                // console.log('饼状图', data.data.chartThree.chartData)
                let myChart = $echarts.init(document.getElementById("myEchartsThree"));

                myChart.setOption({
                    legend: {
                        top: 'bottom'
                    },
                    tooltip: {
                        show: true,
                    },
                    series: [
                        {

                            type: 'pie',
                            radius: [10, 100],//饼图的半径数组,第一项是内半径，第二项是外半径
                            center: ['50%', '45%'],//饼图的中心（圆心）坐标，数组的第一项是横坐标，第二项是纵坐标。
                            roseType: 'area',//设置成玫瑰图
                            itemStyle: {
                                borderRadius: 10
                            },
                            data: data.data.chartThree.chartData
                        }
                    ]
                })
            })
        })
        return {
            getState, data,
        }
    }
};
</script>

<style lang="less" scoped>
h2 {
    height: 0.6rem;
    color: #fff;
    line-height: 0.6rem;
    text-align: center;
    font-size: 0.25rem;
}

.chart {
    height: 4.5rem;
}
</style>
