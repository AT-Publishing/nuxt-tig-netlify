<template>
  <section class="container">
    <h1 class="article">{{ object.title }}</h1>
    <div v-html="object.content" class="article"></div>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  validate ({ params }) {
    return params
  },
  asyncData ({ params, error }) {
    console.log(params)
    return axios.get(`https://api.cosmicjs.com/v1/this-is-g/object/${params.slug}`)
    .then((res) => res.data)
    .catch(() => {
      error({ message: 'XX not found', statusCode: 404 })
    })
  }
}
</script>

<style scoped>
.article {
  max-width: 45%;
  margin: 0 auto;
  text-align: left;
}
</style>
