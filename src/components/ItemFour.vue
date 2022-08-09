<template>
    <div>
        <h2>产品库存</h2>
        <div class="chart" id="myEchartsFour">

        </div>
    </div>
</template>

<script>
import { reactive, inject, onMounted } from "vue"
export default {
    setup() {
        let $echarts = inject('echarts')
        let $http = inject('axios')
        let data = reactive({})

        async function getState() {
            data = await $http({ url: '/four/data' })
        }

        onMounted(() => {
            getState().then(() => {
                console.log('柱状图4', data.data.chartFour.chartData)
                let myChart = $echarts.init(document.getElementById('myEchartsFour'))
                myChart.setOption({
                    gird:{
                        left:"5%",
                        right:"4%",
                        bottom:"3%",
                        containLabel:true,//包含坐标轴
                    },
                    xAxis: {
                        type: "category",
                        axisLine: {
                            lineStyle: {
                                color: "#fff"
                            }
                        },
                        data: data.data.chartFour.chartData.day
                    },
                    yAxis: {
                        type: "value",
                        axisLine: {
                            lineStyle: {
                                color: "#fff"
                            }
                        },
                    },
                    legend: {

                    },
                    tooltip: {
                        trigger: "axis",
                        axisPointer: {
                            type: "shadow"
                        }
                    },
                    series: [
                        {
                            name: "服饰",
                            type: "bar",
                            data: data.data.chartFour.chartData.num.Clothes,
                            stack: 'total',
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "数码",
                            type: "bar",
                            data: data.data.chartFour.chartData.num.digit,
                            stack: 'total',
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "家电",
                            type: "bar",
                            data: data.data.chartFour.chartData.num.Electrical,
                            stack: 'total',
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "家居",
                            type: "bar",
                            data: data.data.chartFour.chartData.num.gear,
                            stack: 'total',
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },

                        {
                            name: "日化",
                            type: "bar",
                            data: data.data.chartFour.chartData.num.Chemicals,
                            stack: 'total',
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },



                    ]
                })
            })
        })

        return {
            getState, data
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
