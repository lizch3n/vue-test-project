<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <HelloWorld msg="Welcome to Your Vue.js App" v-bind:questions="questions" v-bind:answers="answers" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
const questions = require('./questions.js').default;
const answers = require('./answermap.js').default;
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data: function(){
    return {
        questions: questions,
        answers:answers
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
