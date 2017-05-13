<template>
  <div>
  <section class="container">
    <article>
      <about-content />
      <nuxt-link class="button" to="/">
        Home page
      </nuxt-link>
    </article>
  </section>
  <my-hero />
</div>
</template>
<script>
import AboutContent from '~components/AboutContent.vue'
import MyHero from '~components/Hero.vue'

export default {
  components: {
    AboutContent, MyHero
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
