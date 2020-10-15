<template>
  <div class="chart">
    <div class="chart__header">
      <p>My chart</p>
    </div>
    
    <div class="chart__content">
      <div class="chart__y"></div>
      <div v-for="(item,index) of data" :key="index"
        :style="{
          'text-align': 'center',
          'marginTop': (resolutionHeight - dataDecorator[index].calculatedHeightPercent * resolutionHeight) + 'px'
        }"
      >
        <div>
          <label>{{item.value}}</label>
        </div>
        <div 
        class="chart__item" 
        :class="'item_'+index"
        :style="{
          'backgroundColor': item.color, 
          width: widthColumn+'px', 
          display: 'flex',
          'marginLeft': (widthColumn/2)+'px',
          'marginRight': (widthColumn/2)+'px',
          height: (dataDecorator[index].calculatedHeightPercent * resolutionHeight) + 'px',
          }"
        ></div>         
      </div>
    </div>
    <div class="chart__x">
      <div v-for="(item,index) of data" :key="index"
        :style="{
          width: widthColumn+'px',
          'marginLeft': (widthColumn/2)+'px',
          'marginRight': (widthColumn/2)+'px', 
        }"
        >
        <p>{{item.name}}</p>
      </div>
    </div>
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
  data() {
    return {
       columnSize: this.data.length,
       resolutionWidth: null,
       resolutionHeight: null,
       widthColumn: null,

    }
  },
  methods: {
    calculateHeight(){
      let max = 0;
      for(let i = 0; i < this.data.length; i++){
        if(this.data[i].value > max){
          max = this.data[i].value;
        }
      }

      for(let i=0; i < this.data.length; i++){
        this.dataDecorator[i] = {};
        this.dataDecorator[i].calculatedHeightPercent = parseFloat(this.data[i].value/max)
      }
    }
  },
  computed: {
    dataDecorator: function(){
      let max = 0;
      for(let i = 0; i < this.data.length; i++){
        if(this.data[i].value > max){
          max = this.data[i].value;
        }
      }
      var dataDecorate = {};
      for(let i=0; i < this.data.length; i++){
        dataDecorate[i] = {};
        dataDecorate[i].calculatedHeightPercent = parseFloat(this.data[i].value/max)
      }
      return dataDecorate;
    }
  },
  mounted() {
    this.resolutionWidth = window.innerWidth - 200;
    this.resolutionHeight = window.innerHeight - 200;
    this.widthColumn = this.resolutionWidth / (this.columnSize * 2);
    this.calculateHeight();
  },
  watch: {
    dataDecorator: {
      immediate: true,
      handler(newVal, oldVal) {
        //this.widthColumn = this.resolutionWidth / (this.columnSize * 2);
        this.calculateHeight();
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.chart__item {
  //height: 100px;
  //width: 100px;
  position: relative;
}
.chart__header {
  text-align: center;
}
.chart__content {
  display: -webkit-box;

}
.chart__y {
  border: 1px;
  border-color: black;
  width: 1px;
  border-style: solid;
  margin-left: 50px;
}
.chart__x {
  border: 1px;
    border-color: black;
    height: 1px;
    border-style: solid;
    margin-left: 50px;
    display: flex;
    text-align: center;
}
</style>