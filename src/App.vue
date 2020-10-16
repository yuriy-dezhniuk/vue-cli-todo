<template>
  <div id="app">
    <todolist />
  </div>
</template>

<script>

import todolist from './components/todolist.vue';

export default {
  name: 'App',
  components: {
    todolist,
  },
};

</script>

<style lang="scss">
body {
  font-size: 16px;
  color: gray;
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  font-size: 16px;
  margin: 0 auto;
  max-width: 1200px;
  padding: 20px;
  min-height: 100vh;
}
</style>
