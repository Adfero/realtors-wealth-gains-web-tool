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
html, body {
  overflow-x: hidden;
  overflow-y: scroll;
  height: 100%;
}
#hom-main {
  background: $color_white;
  margin: 0 auto;
  padding: 2rem 0;
}
#app, #wealth-gains-container-additional {
  p {
    font-size: 2rem;
  }
  .disclaimer p {
    font-size: 1.5rem;
    font-style: italic;
    text-align: left;
  }
  // :not(.swp_social_panel) {
    h1, h2, h3, h4, p, span {
     color: $color_blue;
   }
  // }
  h2, h3 {
    text-transform: uppercase;
  }
  a.btn {
    padding: 10px 20px;
    height: auto;
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
      color: $color_blue;
    }
  // }
  .illustration.realtor {
    position: absolute;
    bottom: 0;
    left: 3rem;
    top: auto;
    right: auto;
    @media all and (max-width: $screen-md) {
      left: 0;
      img {
        max-width: 75%;
      }
    }
    .speech-bubble {
      position: absolute;
      top: -25px;
      right: -125px;
      @media all and (max-width: $screen-md) {
        display: none;
      }
    }
  }
}
#wealth-gains-container-additional {
  margin: 3rem;
  @media all and (min-width: $screen-xl) {
    margin: 3rem 0;
  }
  p {
    font-size: 2.1rem;
    color: $color_dark_gray;
  }
  .additional-buttons > div {
    padding: 10px 0;
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
      // height: 84px;
      @media all and (min-width: $screen-lg) {
        font-size: 24px;
        // height: 90px;
      }
    }
  }

}

</style>
