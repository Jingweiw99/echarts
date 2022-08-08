<template>
    <div class="chart">

      <slot></slot>  
    </div>
</template>

<script>
export default {
    name: 'ItemChart',
    data() {
        return {

        };
    },
    methods: {

    },
};
</script>

<style lang="less" scoped>
.chart{
  height:5.125rem;
  border: 1px solid blue;
  margin:.25rem;
  background-color: rgba(12,130,255,.85);
}
</style>
