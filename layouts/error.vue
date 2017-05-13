<template>
  <div>
  <section class="container">
    <h1 class="title">
      {{ error.statusCode }}
    </h1>
    <h2 class="info">
      {{ error.message }}
    </h2>
    <nuxt-link class="button" to="/" v-if="error.statusCode === 404">
      Homepage
    </nuxt-link>
  </section>
  <my-hero />
</div>
</template>
<script>
import MyHero from '~components/Hero.vue'

export default {
  props: ['error'],
  components: {
    MyHero
  }
}
</script>

<style scoped>
.title
{
  margin: 50px;
  font-size: 5em;
}
.info
{
  font-weight: 300;
  color: #9aabb1;
  margin: 50px;
}
.button
{
  margin: 50px;
}
</style>
