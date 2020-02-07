<template>
    <div class="wrapper">
        <div class="header">
            <div class="title">{{ title }}</div>
            <div class="controllers">
                <i @click="addNewWrapper()" class="fas fa-plus-square plus"></i>
                <i class="fas fa-window-close cross"  @click="deleteWrapper()"></i>
            </div>
        </div>
        <div class="content-wrapper">
            <child-component
                v-for="(data,index) in childComponent"
                :key="data"
                :child-data="data"
                :title="data.index"
                :actual-index="index"
                v-on:add-new-child-wrapper="addNewChildWrapper" 
                v-on:delete-child-wrapper="deleteChildWrapper"
                >
            </child-component>
        </div>
    </div>
</template>

<script>
import childComponent from './childWrapper.vue'

export default {
    props:{
        mainData: {
           
        },
        title:{
        },
        actualIndex:{
            type:Number
        }
    },
    components:{
        'child-component': childComponent
    },
    data() {
        return {
            childComponent: []
        }
    },
    mounted(){
        this.init();
    },
    methods:{
        init() {
            this.childComponent.push({
                index: this.random()
            });
        },
        random(){
            return Math.round(((Math.random()*100)%100));
        },
        addNewWrapper(){
            this.$emit("add-new-wrapper",{index: this.actualIndex});
        },
        deleteWrapper(){
            this.$emit("delete-wrapper",{index: this.mainData.index});
        },
        deleteChildWrapper({index}){
            this.childComponent = this.childComponent.filter(data => {
                if(data.index == index){
                    return false;
                } return true;
            })
        },
        addNewChildWrapper({index}){
            this.childComponent = [...this.childComponent.slice(0,index+1),{
                index: this.random()
            },...this.childComponent.slice(index+1)]
        }
    }
}
</script>

<style lang="scss" scoped>
.wrapper{
    border: 1px solid black;
    border-radius: .5rem;
    padding: 1rem;
    background: #dbf3fc;
    box-shadow: 0 2px 11px 3px #757575;
    .header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        .title{
            font-size: 2rem;
            font-weight: 900;
        }
        .controllers{
            display: flex;
            background: white;
            padding: .25rem .5rem;
            border-radius: .5rem;
            border: 1px solid #757575;
            box-shadow: 0 5px 5px 1px #757575;
            >i{
                padding:0 .5rem;
                font-size: 1.75rem;
            }
            .plus{
                cursor: pointer;
            }
        }
        
    }
    .content-wrapper{
        display: flex;
        flex-direction: column;
        align-items: center;
    }
}
</style>


