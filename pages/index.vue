<template>
  <section>

  <section class="container">
    <h1 class="title">
      Universal Vue.js Application Framework
    </h1>
    <nuxt-link class="button" to="/about">
      About page
    </nuxt-link>
    </section>
    <my-hero/>

  </section>
</template>

<script>
import MyHero from '~components/Hero.vue'

export default {
  components: {
    MyHero
  }
}

</script>

<style scoped>
.title
{
  margin: 50px 0;
}
</style>
