<template>
    <button
     @click="onClick()" :style="{ background: color}"
    class="btn">{{ text }}</button>
</template>
<script>
export default {
    name:"button",
    //for the colored button to be effective we add props
    // before adding double  braces to the button class 
    //removing the add task test
    //for the color,we add a v-bind
    // next is adding a method after the onclick props
props:{
    text: String,
    color:String
},
methods: {
    onClick(){
        this.$emit('btn-click')
    },
}
}
</script>
<style scoped>

</style>