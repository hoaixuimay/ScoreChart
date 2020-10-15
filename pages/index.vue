<template>
  <div class="container">
    <div class="input">
      <div v-for="sub in data" :key="sub.name">
        <p>{{sub.name}}</p>
        <input type="text" v-model="sub.value">
        <input type="text" v-model="sub.color">
      </div>
    </div>
    <br/>
    <chart :data="data"></chart>
  </div>
</template>

<script>
import Chart from "~/components/BarChart.vue";
export default {
  components: {
    Chart,
  },
  data() {
    return {
      data: [
        { name: "Math", value: 6, color: "red" },
        { name: "Literature", value: 5.5, color: "blue" },
        { name: "Physics", value: 3, color: "#33cc33" },
        { name: "Chemistry", value: 0, color: "orange" },
        { name: "English", value: 3, color: "black" },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
.container {
  margin: 10px;
  display: flex;
}
</style>