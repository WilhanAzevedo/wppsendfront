<template>
  <div id="app">
    <div class="root">
      <router-view />
  </div>
    
  
  </div>
</template>

<script>


export default {
  name: 'App',
  
}
</script>

<style>

.root{
  height: 100vh;
  width: 100vw;
  /* display: flex; */
  flex-direction: column;
  /* justify-content: center; */
  align-items: center;
}

 #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* background: linear-gradient(to bottom, #fdfdfd 0%, #dd994a 50%, #EB7C00 100%); */
  height: 100vh;
}

</style>
