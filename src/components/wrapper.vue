<template>
    <div class="wrapper">
        <div class="header">
            <div class="title">{{ title }}</div>
            <div @click="addNewWrapper()" class="plus">+</div>
            <div @click="deleteWrapper()" class="cross">X</div>
        </div>
        <div class="content-wrapper">
            <div class="content" v-for="data in mainData" :key="data">
                <div class="text">{{ data }}</div>
                <div class="addNewSubChild" @click="addNewSubChild()">+</div>
            </div>
        </div>
    </div>
</template>

<script>
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
    data() {
        return {
            
        }
    },
    methods:{
        addNewWrapper(){
            this.$emit("add-new-wrapper",{index: this.actualIndex});
        },
        deleteWrapper(){
            this.$emit("delete-wrapper",{index: this.mainData.index});
        }
    }
}
</script>

<style lang="scss" scoped>
.wrapper{
    border: 1px solid black;
    .header{
        display: flex;
        justify-content: space-between;
        background: white;
        padding:1rem;
        .plus{
            padding: 1rem;
            background: yellow;
            cursor: pointer;
        }
    }
    .content-wrapper{
        display: flex;
    }
}
</style>


