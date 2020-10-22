<template>
  <svg class="barchart" :width="width" :height="height"></svg>
</template>
<script>
  export default {
    name: "BarChart",
    props: ['dataset','selected'],
    mounted() {
      console.log('data set is looking grim we need to clean it',this.dataset)
    }
  };
</script>

<style lang="scss">
</style>
