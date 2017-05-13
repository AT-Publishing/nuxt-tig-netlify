<template>
  <section class="container content">
    <all-posts />
  </section>
</template>

<script>
import AllPosts from '~components/PostsFundamentals.vue'

export default {
  components: {
    AllPosts
  },
  head () {
    return {
      title: `Fundamentals In Bitcoin Trading | This Is Gentlemen `
    }
  }
}
</script>

<style scoped>

</style>
