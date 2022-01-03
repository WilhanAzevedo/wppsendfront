<template>
  <div id="app">
    <div class="home">
      <Home />
    </div>
    
  
  </div>
</template>

<script>
import Home from './components/Home.vue'


export default {
  name: 'App',
  components: {
    Home,
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
  background: linear-gradient(to bottom, #fdfdfd 0%, #dd994a 50%, #EB7C00 100%);
  height: 100vh;
}

.home {
  max-width: 700px;
  margin: 0 auto;
  text-align: left;
}

</style>
