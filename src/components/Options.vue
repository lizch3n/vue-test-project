<template>
    <div>
        <button v-on:click="selectOption" :id="Object.keys(answer)[0]">{{Object.keys(answer)[0]}}</button>
    </div>
</template>

<script>
    export default {
        name: 'Options',
        props: {
            msg: String,
            answer: Object,
        },
        data: function(){
            return {
            }
        },
        methods: function(){
            const selectOption = function(evt){
                this.$emit('clicked', {"val":evt.target.id});
            }
            return {
                selectOption:selectOption
            }
        }(this)
    }
</script>

<style>

</style>