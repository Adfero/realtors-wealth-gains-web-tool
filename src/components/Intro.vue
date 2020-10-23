<template>
  <div class="intro-container">
    <h2>Building Wealth Through Homeownership</h2>
    <p>Owning a home is one of the best ways you can build wealth for yourself and future generations. Follow the prompts to see how much wealth you can build by purchasing a home in different areas in the U.S.</p>
    <a class="intro-next btn-blue btn" @click="$emit('close')">Next</a>
  </div>
</template>

<script>
export default {
  name: 'intro'
}
</script>
