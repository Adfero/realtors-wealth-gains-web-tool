<template>
  <div class="intro-container">
    <h2>Building Wealth Through Homeownership</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris pulvinar, ligula vitae malesuada interdum, nibh nisl porttitor metus, sit amet varius tortor lacus eget neque. Suspendisse sagittis velit ac risus tempus, sit amet posuere sapien venenatis. Nam eget turpis feugiat, semper eros eget, finibus lectus. Praesent scelerisque nisl vel sodales consequat. Nam ante augue, fermentum ac justo vel, eleifend convallis dui. Duis iaculis ex et fringilla elementum.</p>
    <a class="intro-next button" @click="$emit('close')">Next</a>
  </div>
</template>

<script>
export default {
  name: 'intro'
}
</script>
