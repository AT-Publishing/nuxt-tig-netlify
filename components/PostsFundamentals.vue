<template>
  <section>
    <div class="">

      <article v-for="item in this.posts">
      <h2 v-bind:id="item.slug" class="article">
        <a v-bind:href="item.slug | hash">
          {{item.title}}
        </a>
      </h2>
      <p class="time article">
        <small v-if="item.created_at">Published: {{item.created_at | moment}}</small>
        <small v-if="item.modified_at">Updated: {{item.modified_at | moment}}</small>
      </p>
      <div v-html="item.content" class="article"></div>
     </article>

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
    },
    hash: function (str) {
      return "#"+str
    }
  },
  created () {
    axios.get(`https://api.cosmicjs.com/v1/this-is-g/object-type/fundamentals`, cache('5 minutes'))
    .then(response => {
      this.posts = response.data.objects
    })
    .catch(e => {
      this.errors.push(e)
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
