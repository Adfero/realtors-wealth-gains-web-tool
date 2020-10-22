<template>
  <div id="app">
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
h1, h2, p, span {
  color: #165A86;
}
h2 {
  text-transform: uppercase;
  font-size: 22px;
  color: #165A86;
  font-weight: 600;
}
a.button {
  cursor: pointer;
  color: white;
  font-weight: bold;
  background: #165A86;
  padding: 10px 15px;
  border-radius: 10px;
}
a.button:hover {
  color: white;
}
input, select {
  color: #165A86;
}
</style>
