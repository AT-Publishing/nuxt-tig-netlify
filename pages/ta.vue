<template>
  <section class="container">
    <img src="../assets/img/logo.png" alt="Nuxt.js Logo" class="logo" />
    <h1 class="title">
      tits&ass here
    </h1>
    <all-posts />
    <nuxt-link class="button" to="/">Home</nuxt-link>
  </section>
</template>
<script>
import AllPosts from '~components/PostsTechnicals.vue'

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
