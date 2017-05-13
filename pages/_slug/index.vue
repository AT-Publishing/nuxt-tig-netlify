<template>
  <section>
  <h1>Cosmic</h1>
  <main :key="page.slug">
    <div class="container" v-html="page.content"></div>
  </main>
</section>
</template>

<script>
import Cosmic from '~plugins/cosmic'
export default {
  async data ({ params }) {
    let res
    try {
      res = await Cosmic.getPage(params.slug || 'home')
    } catch (e) {
      res = await Cosmic.getPage('error')
    }
    return { page: res.object }
  },
  head () {
    return {
      title: this.page.title
    }
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  margin-top: 5px;
  max-width: 960px;
  padding: 15px;
  padding-bottom: 40px;
}
</style>
