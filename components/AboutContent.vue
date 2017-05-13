<template>
  <section>
    <div class="container">
      <h2>{{this.posts.title}}</h2>
      <div v-html="this.posts.content"></div>
    </div>
  </section>
</template>

<script>
import moment from 'moment'
import axios from 'axios'
import apicache from 'apicache'
let cache = apicache.middleware
export default {
  name: 'home',
  data () {
    return {
      posts: []
    }
  },
  filters: {
    moment: function (str) {
      var d = new Date(str)
      if (moment(d).isValid()) {
        return moment(d).format('MMMM Do \'YY, h:mm a')
      } else {
        return '...'
      }
    }
  },
  created () {
    axios.get(`https://api.cosmicjs.com/v1/this-is-g/object/about?locale=en`, cache('5 minutes'))
    .then(response => {
      this.posts = response.data.object
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

<style scoped>
</style>
Contact GitHub API Training Shop Blog About
