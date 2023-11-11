<template>
  <div id="app">
    <TodoCreator/>
  </div>
</template>

<script>
import TodoCreator from './components/TodoCreator.vue';

export default {
  name: 'App',
  components: {
    TodoCreator
  }
}
</script>

<style>
html {
  background-color: #1a202b;
  width: 100%;
  height: 100%;
  color: white;
}

body {
  width: 100%;
  height: 100%;
  display: flex;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
}
</style>
