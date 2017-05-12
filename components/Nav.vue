<template>
  <nav class="nav">
    <ul>
      <li>
        <my-winkdex />
      </li>
      <li>
        <nuxt-link to="/" exact>Home</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/news">In the news</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/" active-class="none"><i class="logo"></i></nuxt-link>
      </li>
      <li>
        <nuxt-link to="/fundamentals">Fundamentals</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/ta">Technicals</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/about">About</nuxt-link>
      </li>
    </ul>
  </nav>
</template>

<script>
import MyWinkdex from '~components/Winkdex.vue'

export default {
  components: {
    MyWinkdex
  }
}
</script>

<style>
.nav {
  height: 60px;
  position: absolute;
  text-align: center;
  width: 100%;
  z-index: 1;
}
</style>
