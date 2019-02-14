<template>
  <div id="app">
    <TimeLine></TimeLine>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TimeLine from './components/TimeLine'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TimeLine
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
}

body {
  margin: 0px;
}
</style>
