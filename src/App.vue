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
  // :not(.swp_social_panel) {
    h1, h2, h3, h4, p, span:not(.swp_share) {
     color: $color_navy;
   }
  // }
  h2, h3 {
    text-transform: uppercase;
  }
  a.btn {
    cursor: pointer;
    color: white;
    font-weight: bold;
    border-radius: 10px;
    font-size: 20px;
    font-family: $font_brandon_bold;
    text-transform: uppercase;
  }
  // :not(.swp_social_panel) {
    input, select {
      color: $color_navy;
    }
  // }
}
#wealth-gains-container-additional {
  p {
    font-size: 2.1rem;
    color: $color_dark_gray;
  }
  .additional-buttons > div {
    padding: 5px 0;
    @media all and (min-width: $screen-md) {
      padding: 0 5px;
    }
    @media all and (min-width: $screen-lg) {
      padding: 0 15px;
    }
    &:first-child {
      @media all and (min-width: $screen-md) {
        padding-left: 0;
      }
    }
    &:last-child {
      @media all and (min-width: $screen-md) {
        padding-right: 0;
      }
    }
    a.btn {
      font-size: 2rem;
      @media all and (min-width: $screen-lg) {
        font-size: 24px;
      }
    }
  }

}

</style>
