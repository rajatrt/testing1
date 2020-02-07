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
    },
    addNewWrapper({index}){
      this.mainData = [...this.mainData.slice(0,index+1),{
        index: this.title()
      },...this.mainData.slice(index+1)]
    },
  }
}
</script>
<style lang="scss" scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  >div{
    margin:1rem;
  }
  >div:last-child{
    margin-bottom:0;
  }
}
</style>
