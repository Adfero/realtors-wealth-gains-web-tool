<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <WebTool/>
  </div>
</template>

<script>
import WebTool from './components/WebTool'

export default {
  name: 'App',
  components: {
    WebTool
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
.button {
  cursor: pointer;
  color: white;
  font-weight: bold;
  background: blue;
  padding: 10px 15px;
  border-radius: 10px;
}
</style>
