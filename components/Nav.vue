<template>
  <nav class="nav">
    <ul>
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
    </ul>
  </nav>
</template>

<style>
.nav {
  height: 60px;
  position: absolute;
  text-align: center;
  width: 100%;
  z-index: 1;
}
</style>
