<template>
  <section class="container content">
    <all-posts />
  </section>
</template>

<script>
import AllPosts from '~components/PostsTechnicals.vue'

export default {
  components: {
    AllPosts
  },
  head () {
    return {
      title: `Technical Analysis for Bitcoin Traders | This Is Gentlemen `
    }
  }
}
</script>

<style scoped>

</style>
