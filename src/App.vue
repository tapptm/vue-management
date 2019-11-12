<template>
  <div id="app">
    <manage msg="Account Management"/>
   
    </div>
</template>

<script>

import manage from './components/Management.vue'


export default {
  name: 'app',
  
  components: {
    manage,
    
  },
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
