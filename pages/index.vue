<template>
  <section>
   <section class="container">

    <div class="center">
      <div class="side">

        <my-bar />


      </div>
      <div class="main">

        <script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script><ins class="adsbygoogle" style="display:inline-block;width:728px;height:90px" data-ad-client="ca-pub-6979812205705127" data-ad-slot="6506986898"></ins><script>(adsbygoogle = window.adsbygoogle || []).push({});</script>
        <all-posts />

      </div>
    </div>


   </section>
   <my-hero/>
  </section>
</template>

<script>
import MyHero from '~components/Hero.vue'
import MyBar from '~components/Bar.vue'
import AllPosts from '~components/PostsContent.vue'

export default {
  props: ['page'],
  components: {
    MyHero, AllPosts, MyBar
  }
}
</script>

<style scoped>
</style>
