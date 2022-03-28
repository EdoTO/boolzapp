<template>
  <div id="app">
    
    <Boolzapp/>
    
  </div>
</template>

<script>
import Boolzapp from './components/Boolzapp.vue'

export default {
  name: 'App',
  components: {
    Boolzapp,
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
