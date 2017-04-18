<template>
  <div id="app">
    <Bar />
    <router-view class="a"></router-view>
  </div>
</template>

<script>
import Bar from '@/components/Bar'
export default {
  name: 'app',
  components: {
    Bar
  }
}
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.bar {
  background-color: #fff;
  color: #555;
  min-height: 8rem;
  padding: 0 2rem;
  z-index: 10;
  position: fixed;
}
</style>
