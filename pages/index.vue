<template>
  <section>
   <section class="container">
    <h1 class="title">
      Recent Posts
    </h1>
    <section>
      <all-posts />
    </section>
    <nuxt-link class="button" to="/about">
      About page
    </nuxt-link>
   </section>
   <my-hero/>
  </section>
</template>

<script>
import MyHero from '~components/Hero.vue'
import AllPosts from '~components/PostsContent.vue'

export default {
  components: {
    MyHero, AllPosts
  }
}

</script>

<style scoped>
.title
{
  margin: 50px 0;
}
</style>
