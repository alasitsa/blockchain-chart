<template>
  <BlockchainChart/>
</template>

<script>
import BlockchainChart from './components/BlockchainChart.vue'

export default {
  name: 'App',
  components: {
    BlockchainChart
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
