<template>
  <div id="app">
    <QuizComponent />
  </div>
</template>

<script>
import QuizComponent from './components/QuizComponent.vue';

export default {
  name: 'App',
  components: {
    QuizComponent
  }
};
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

