<template>
  <div id="app">
    
    <Sidebar/>
    
  </div>
</template>

<script>
import Sidebar from './components/Sidebar.vue'

export default {
  name: 'App',
  components: {
    Sidebar,
  },
}
</script>

<style lang="scss">

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  width: 100vw;
  display: flex;
}

body {
  display: flex;
  width: 100vw;
}

.sidebar {
  width: 30%;
}

.chat {
  width: 70%;
}

</style>
