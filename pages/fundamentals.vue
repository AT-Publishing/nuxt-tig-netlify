<template>
  <section class="container">
    <h1 class="title">
      Volatility and Books here
    </h1>
    <all-posts />
    <nuxt-link class="button" to="/">Home</nuxt-link>
  </section>
</template>

<script>
import AllPosts from '~components/PostsFundamentals.vue'

export default {
  components: {
    AllPosts
  }
}
</script>

<style scoped>
.title
{
  margin: 50px 0;
}
</style>
