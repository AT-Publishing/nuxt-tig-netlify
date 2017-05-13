<template>
  <section>

      <article v-for="item in this.posts">
      <h2 class="feed">{{item.title}}</h2>
      <div>

        <div v-if="item.metadata.feature"  class="thumb">
          <img v-bind:src="item.metadata.feature.url">
        </div>
        <div class="desc">
          <div class="time">
            <small v-if="item.created_at"><time v-bind:datetime="item.created_at">Published: {{item.created_at | moment}}</time></small>
            <small v-if="item.modified_at"><time v-bind:datetime="item.modified_at">Updated: {{item.modified_at | moment}}</time></small>
          </div>
          <!-- make excerpt -->
          <p><vue-markdown :source="item.metadata.description"></vue-markdown></p>
          <p>
            <!-- https://api.cosmicjs.com/v1/this-is-g/object/post-with-image -->
            <a v-bind:href="item.slug" class="morelink">Read more</a>
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
