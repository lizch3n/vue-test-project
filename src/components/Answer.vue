<template>
    <div >
        <h2>{{Object.keys(answer)[0]}}</h2>
        <p>{{answer.copy[0]}}</p>
        <p>{{answer.copy[1]}}</p>
    </div>
</template>

<script>
    export default {
        name: 'Answer',
        props: {
            msg: String,
            answer: Object,
        },
        data: function(){
            return {
            }
        },
        methods: function(){
            return {

            }
        }(this)
    }
</script>

<style>

</style>