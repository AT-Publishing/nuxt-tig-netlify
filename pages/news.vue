<template>
  <section class="container">

    <h1 class="title">
      Searchable News
    </h1>
    <script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script><ins class="adsbygoogle" style="display:inline-block;width:728px;height:90px" data-ad-client="ca-pub-6979812205705127" data-ad-slot="6506986898"></ins><script>(adsbygoogle = window.adsbygoogle || []).push({});</script>

    <my-news-api />

    <p>Data via NewsApi.org</p>
    <nuxt-link class="button" to="/">Home</nuxt-link>
    
  </section>
</template>
<script>
import MyNewsApi from '~components/NewsApi.vue'

export default {
  components: {
    MyNewsApi
  },
  head () {
    return {
      title: `Searchable News | This Is Gentlemen `
    }
  }
}
</script>
<style scoped>
.title
{
  margin: 30px 0;
}
</style>
