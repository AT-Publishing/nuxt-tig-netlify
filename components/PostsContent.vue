<template>
  <section>
    <div class="container">

      <article v-for="item in this.posts">
      <h2>{{item.title}}</h2>
      <div>
        <vue-markdown :source="item.content"></vue-markdown>
        <small v-if="item.created_at">Published: {{item.created_at | moment}}</small>
        <small v-if="item.modified_at">&nbsp;|&nbsp;Updated: {{item.modified_at | moment}}</small>
      </div>
     </article>

    </div>
  </section>
</template>

<script>
import moment from 'moment'
import axios from 'axios'
import apicache from 'apicache'
import VueMarkdown from 'vue-markdown'
let cache = apicache.middleware
export default {
  name: 'home',
  data () {
    return {
      posts: []
    }
  },
  components: {
    'vue-markdown': VueMarkdown
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
    axios.get(`https://api.cosmicjs.com/v1/this-is-g/object-type/posts`, cache('5 minutes'))
    .then(response => {
      if (response.data.objects.length > 4) {
        response.data.objects.slice(4)
      }
      this.posts = response.data.objects
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

<style scoped>

</style>
