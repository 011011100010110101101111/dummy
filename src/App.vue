<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Index />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Index from './components/index'
export default {
  name: 'App',
  components: {
    Index
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
