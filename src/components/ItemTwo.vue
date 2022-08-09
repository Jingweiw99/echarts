<template>
    <div>
        <h2>周销图</h2>
        <div class="chart" id="myEchartsTwo">

        </div>
    </div>
</template>

<script>
import { reactive, onMounted, inject } from 'vue'
export default {
    setup() {
        let $echarts = inject('echarts')
        let $http = inject('axios')
        let data = reactive({})
        async function getState() {
            data = await $http({ url: '/two/data' })
        }


        onMounted(() => {
            getState().then(() => {
                // console.log('折线图', data.data.chartTwo.chartData)
                let myCharts = $echarts.init(document.getElementById("myEchartsTwo"))
                myCharts.setOption(
                    {
                        tooltip: {// 提示框
                            trigger: 'axis',// 坐标轴触发
                            axisPointer:{
                                type:"cross",
                                label:{
                                    backgroundColor:"#e6b660"
                                }
                            }
                        },
                        legend:{
                            data:['服饰','数码','家电','家居','日化']
                        },
                        gird:{
                            left:"1%",
                            right:"4%",
                            bottom:"3%",
                            containLabel:true
                        },
                        xAxis: {//x类目，y值
                            type: "category",
                            boundaryGap: false,
                            axisLine:{
                                lineStyle:{
                                    color:"#fff"
                                }
                            },
                            data: data.data.chartTwo.chartData.day
                        },
                        yAxis: {
                            type: 'value',
                            axisLine:{
                                lineStyle:{
                                    color:"#fff"
                                }
                            },
                        },
                        series: [

                            {
                                name: "服饰",
                                type: 'line',
                                smooth: true,
                                showSymbol: false,
                                stack: "Total",// 数据堆叠
                                areaStyle: {//设置填充区域的样式
                                    opacity: 0.8,
                                    color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                        {
                                            offset: 0,
                                            color: "rgb(128, 255, 165)",
                                        },
                                        {
                                            offset: 1,
                                            color: "rgb(1, 191, 236)",
                                        },
                                    ]),
                                },
                                lineStyle: { // 设置线段样式
                                    width: 0,
                                },
                                emphasis: {//设置高亮的图形样式和标签样式 
                                    focus: "series",//只显示选中的内容高亮
                                },
                                data: data.data.chartTwo.chartData.num.Clothes
                            },
                            {
                                name: "数码",
                                type: 'line',
                                smooth: true,
                                showSymbol: false,
                                stack: "Total",// 数据堆叠
                                areaStyle: {//设置填充区域的样式
                                    opacity: 0.8,
                                    color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                        {
                                            offset: 0,
                                            color: "rgb(0, 221, 255)",
                                        },
                                        {
                                            offset: 1,
                                            color: "rgb(77, 119, 255)",
                                        },
                                    ]),
                                },
                                lineStyle: { // 设置线段样式
                                    width: 0,
                                },
                                emphasis: {//设置高亮的图形样式和标签样式 
                                    focus: "series",//只显示选中的内容高亮
                                },
                                data: data.data.chartTwo.chartData.num.Electrical
                            },
                            {
                                name: "家电",
                                type: 'line',
                                smooth: true,
                                showSymbol: false,
                                stack: "Total",// 数据堆叠
                                areaStyle: {//设置填充区域的样式
                                    opacity: 0.8,
                                    color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                        {
                                            offset: 0,
                                            color: "rgb(55, 162, 255)",
                                        },
                                        {
                                            offset: 1,
                                            color: "rgb(116, 21, 219)",
                                        },
                                    ]),
                                },
                                lineStyle: { // 设置线段样式
                                    width: 0,
                                },
                                emphasis: {//设置高亮的图形样式和标签样式 
                                    focus: "series",//只显示选中的内容高亮
                                },
                                data: data.data.chartTwo.chartData.num.digit
                            },
                            {
                                name: "家居",
                                type: 'line',
                                smooth: true,
                                showSymbol: false,
                                stack: "Total",// 数据堆叠
                                areaStyle: {//设置填充区域的样式
                                    opacity: 0.8,
                                    color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                        {
                                            offset: 0,
                                            color: "rgb(255, 0, 135)",
                                        },
                                        {
                                            offset: 1,
                                            color: "rgb(135, 0, 157)",
                                        },
                                    ]),
                                },
                                lineStyle: { // 设置线段样式
                                    width: 0,
                                },
                                emphasis: {//设置高亮的图形样式和标签样式 
                                    focus: "series",//只显示选中的内容高亮
                                },
                                data: data.data.chartTwo.chartData.num.gear
                            },
                            {
                                name: "日化",
                                type: 'line',
                                smooth: true,
                                showSymbol: false,
                                stack: "Total",// 数据堆叠
                                areaStyle: {//设置填充区域的样式
                                    opacity: 0.8,
                                    color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                        {
                                            offset: 0,
                                            color: "rgb(255, 191, 0)",
                                        },
                                        {
                                            offset: 1,
                                            color: "rgb(224, 62, 76)",
                                        },
                                    ]),
                                },
                                lineStyle: { // 设置线段样式
                                    width: 0,
                                },
                                emphasis: {//设置高亮的图形样式和标签样式 
                                    focus: "series",//只显示选中的内容高亮
                                },
                                data: data.data.chartTwo.chartData.num.Chemicals
                            },

                        ]

                    }
                )
            })
        })
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
