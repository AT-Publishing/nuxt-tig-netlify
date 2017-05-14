<template>
  <section>

      <article v-for="item in this.posts">
      <h2 class="feed">{{item.title}}</h2>
      <div>

        <div v-if="item.metadata.feature"  class="thumb">
          <nuxt-link :to="item.slug">
            <img v-bind:src="item.metadata.feature.url">
          </nuxt-link>
        </div>
        <div class="desc">
          <div class="time">
            <!-- how to backdate though? -->
            <small v-if="item.created_at"><time v-bind:datetime="item.created_at">Published: {{item.created_at | moment}}</time></small>
            <small v-if="item.modified_at"><time v-bind:datetime="item.modified_at">Updated: {{item.modified_at | moment}}</time></small>
          </div>
          <!-- excerpt -->
          <p v-html="item.metadata.description"></p>
          <p>
            <nuxt-link class="morelink" :to="item.slug">Read more</nuxt-link>
          </p>
        </div>



      </div>
     </article>

  </section>
</template>

<script>
  import moment from 'moment'
  import axios from 'axios'
  import apicache from 'apicache'
  let cache = apicache.middleware
  export default {
    name: 'home',
    props: ['page'],
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
      axios.get(`https://api.cosmicjs.com/v1/this-is-g/object-type/posts?hide_metafields=true`, cache('5 minutes'))
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
