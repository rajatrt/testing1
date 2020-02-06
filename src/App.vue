<template>
  <div id="app">
    <Wrapper 
      v-for="(data,index) in mainData"
      :key="data"
      :title="data.index"
      :actual-index="index"
      v-on:add-new-wrapper="addNewWrapper" 
      v-on:delete-wrapper="deleteWrapper" 
      :main-data="data" :index="data.index"></Wrapper>
  </div>
</template>

<script>
import Wrapper from './components/wrapper.vue'

export default {
  name: 'app',
  components: {
    Wrapper
  },
  data() {
    return {
      mainData:[]
    }
  },
  mounted(){
    this.init();
  },
  methods:{
    title(){
      return Math.round(((Math.random()*100)%100));
    },
    init() {
      this.mainData.push({
        index: this.title()
      });
    },
    deleteWrapper({index}){
      this.mainData = this.mainData.filter(data => {
        if(data.index == index){
          return false;
        } return true;
      })
      // let newData=[];
      // window.console.log("-->>",this.mainData);
      // let count = 1;
      // for(let i in this.mainData){
      //   window.console.log('-->>.',i);
      //   if(this.mainData[i].index != index){
      //     newData.push({
      //       ...this.mainData[i],
      //       index: count++
      //     })
      //   }
      // }
      // window.console.log("-->>>",newData);
      // this.mainData = newData;
    },
    addNewWrapper({index}){
      this.mainData = [...this.mainData.slice(0,index),{
        index: this.title()
      },...this.mainData.slice(index)]
    },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
