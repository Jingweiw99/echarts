<template>
    <div>
        <header>
            <h1>大数据可视化</h1>
        </header>
        <section class="container">
            <section class="itemLeft">
               
                <item-chart>
                    <item-one />
                </item-chart>
                <item-chart>
                    <item-two />
                </item-chart>
            </section>
            <section class="itemCenter">
                <map-page/>    
            </section>
            <section class="itemRight">
                
                <item-chart>
                    <item-three />
                </item-chart>
                <item-chart>
                    <item-four />
                </item-chart>
            </section>
        </section>

    </div>
</template>

<script>
import ItemChart from '../components/ItemChart.vue'
import ItemOne from '../components/ItemOne.vue'
import ItemTwo from '../components/ItemTwo.vue'
import ItemThree from '../components/ItemThree.vue'
import ItemFour from '../components/ItemFour.vue'
import MapPage from '../components/MapPage.vue'


import { inject } from 'vue'

export default {
    name: 'homePage',
    components: {
        ItemChart,
        ItemOne,
        ItemTwo,
        ItemThree,
        ItemFour,
        MapPage,
    },
    setup(){
        let $echarts = inject('echarts')
        let $http = inject('axios')
        // console.log($echarts)
        // console.log($http)
        return{
            
        }
    }
};
</script>

<style lang="less" scoped>
header {
    height: 1rem;
    width: 100%;
    background-color: rgba(0, 0, 255, .2);

    h1 {
        font-size: 0.375rem;
        color: #fff;
        text-align: center;
        line-height: 1rem;
    }

}

.container {
    min-width: 1200px;
    max-width: 2048px;
    margin: 0 auto;
    // border: 1px solid red;
    padding: .125rem .125rem 0;
    // background-color: gray;
    display: flex;

    .itemLeft {
        flex: 3;
    }

    .itemCenter {
        flex: 5;
        height: 10.5rem;
        border: 1px solid blue;
        padding: 0.125rem;
        margin: .25rem;
    }

    .itemRight {
        flex: 3;
    }
}
</style>
