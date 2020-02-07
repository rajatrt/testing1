<template>
    <div class="child-wrapper">
        <div class="left-child">
            <span class="text">{{ title }}</span>
            <input type="text" placeholder="Enter your name..."/> 
        </div>
        <div class="controllers">
            <i @click="addNewSubChild()" class="fas fa-plus-square plus"></i>
            <i class="fas fa-window-close cross"  @click="deleteChildWrapper()"></i>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        title:{

        },
        childData:{
            type: Object
        },
        actualIndex:{
            type: Number
        }
    },
    methods: {
        addNewSubChild(){
            this.$emit("add-new-child-wrapper",{index: this.actualIndex});
        },
        deleteChildWrapper(){
            this.$emit("delete-child-wrapper",{index: this.childData.index});
        },
    }
}
</script>

<style lang="scss" scoped>
.child-wrapper{
    display: flex;
    width: 100%;
    max-width: 20rem;
}
</style>
