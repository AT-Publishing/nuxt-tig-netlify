<template>
  <section class="container">
    <img src="../assets/img/logo.png" alt="Nuxt.js Logo" class="logo" />
    <h1 class="title">
      Searchable News Here
    </h1>
    <my-news-api />
    <nuxt-link class="button" to="/">Home</nuxt-link>
  </section>
</template>
<script>
import MyNewsApi from '~components/NewsApi.vue'

export default {
  components: {
    MyNewsApi
  }
}
</script>
<style scoped>
.title
{
  margin: 50px 0;
}
</style>
