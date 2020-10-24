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

<style lang="scss">
@import './variables.scss';
@import './utils.scss';
#hom-main {
  background: $color_white;
  margin: 0 auto;
  padding: 2rem 0;
}
#app, #wealth-gains-container-additional {
  p {
    font-size: 2rem;
  }
  h1, h2, h3, h4, p, span {
    color: $color_navy;
  }
  h2, h3 {
    text-transform: uppercase;
  }
  a.btn {
    cursor: pointer;
    color: white;
    font-weight: bold;
    border-radius: 10px;
    font-size: 20px;
    font-family: BrandonGrotesqueWeb-Bold, 'Work Sans', sans-serif;
    text-transform: uppercase;
  }
  input, select {
    color: $color_navy;
  }
}
#wealth-gains-container-additional {
  p {
    font-size: 2.1rem;
    color: $color_dark_gray;
  }
  a.btn {
    font-size: 24px;
  }
}

</style>
