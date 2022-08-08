<template>
    <div>
        <h2>图表1</h2>
        <div class="chart" id="oneChart">
            
        </div>
    </div>
</template>

<script>
import { inject, onMounted, reactive } from 'vue'
export default {
    name: 'ItemOne',
    setup() {
        let $echarts = inject("echarts")
        let $http = inject('axios')

        let data = reactive({})
        let xData = reactive([])
        let yData = reactive([])
        function setData() {
            // console.log(data)
            xData = data.data.chartOne.chartData.map((v) => v.title);
            yData = data.data.chartOne.chartData.map((v) => v.num);
            // console.log(xData, yData)
        }

        async function getState() {
            data = await $http({
                url: "/one/data"
            })
            // console.log(oneData.data.chartOne.chartData)
        }
        onMounted(() => {
            let myChart = $echarts.init(document.getElementById("oneChart"))

            // 请求成功之后调用处理数据的方法
            getState().then(() => {
                setData()
                myChart.setOption({
                    grid: {
                        top: "3%",
                        left: "2%",
                        bottom: "3%",
                        right: "9%",
                        // 包含坐标轴的文字
                        containLabel: true
                    },
                    xAxis: {
                        type: 'value',
                        axisLabel:{
                            color:"#fff"
                        }
                    },
                   
                    yAxis: {
                        type: 'category',
                        data: xData,
                        axisLabel:{
                            color:"#fff"
                        }
                    },
                    series: [
                        {
                            data: yData,
                            type: 'bar',
                            // 图形上面的文字
                            label:{
                                show:true, // 显示数值
                                position:'right',//位置
                                textStyle:{
                                color:'#fff'
                                }
                            },
                            itemStyle: {
                                normal: {
                                    barBorderRadius: [0, 20, 20, 0],
                                    color: new $echarts.graphic.LinearGradient(0, 0, 1, 0, [
                                        {
                                            offset: 0,
                                            color: '#005eaa'
                                        },
                                        {
                                            offset: 0.5,
                                            color: '#339ca8'
                                        },
                                        {
                                            offset: 1,
                                            color: '#cda819'
                                        }
                                    ])

                                }
                            }
                        }
                    ]


                })
                // 让echarts根据浏览器大小改变动态该改变
                window.onresize = function () {
                    myChart.resize()
                }
            })

        })
        return {
            getState,
            xData,
            yData,
            data,
            setData
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
