<template>
  <section class="container">
    <h1 class="title">
      About
    </h1>
    <article>
      <about-content />
    </article>
    <nuxt-link class="button" to="/">
      Home page
    </nuxt-link>
  </section>
</template>
<script>
import AboutContent from '~components/AboutContent.vue'

export default {
  components: {
    AboutContent
  }
}
</script>

<style scoped>
.title
{
  margin-top: 50px;
}
.info
{
  font-weight: 300;
  color: #9aabb1;
  margin: 0;
  margin-top: 10px;
}
.button
{
  margin-top: 50px;
}
</style>
