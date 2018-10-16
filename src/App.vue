<template>
  <div id="app">
    <DataTable msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import DataTable from './components/DataTable.vue'

export default {
  name: 'app',
  components: {
    DataTable
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
