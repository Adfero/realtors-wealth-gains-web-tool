<template>
  <div class="summary">
    <h4>Oh wow you picked {{ selected }}!</h4>
    <p>Here's some summarizing text about your choice and how great it was!</p>
    <a class="button" href="/realtors-wealth-gains-web-tool/">Start Over</a>
  </div>
</template>
<script>
  export default {
    name: "Summary",
    props: ['selected','data'],
    mounted() {
      // console.log('data set is looking grim we need to clean it',this.dataset)
    }
  };
</script>

<style lang="scss">
</style>
