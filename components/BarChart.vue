<template>
  <div class="chart">
    <div class="chart__header"></div>
    <div class="chart__x"></div>
    <div class="chart__content">
      <div class="chart__item" v-for="(item,index) of data" :key="index">
                        {{item}}
                    </div>
    </div>
    <div class="chart__y"></div>
    <div class="chart__footer"></div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Array,
    },
  },
};
</script>

<style scoped>
.chart__item {
  height: 100px;
  width: 100px;
  position: relative;
}
</style>