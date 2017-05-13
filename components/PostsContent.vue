<template>
  <section>

      <article v-for="item in this.posts">
      <h2 class="feed">{{item.title}}</h2>
      <div>

        <div class="thumb">
          <img v-if="item.metadata.feature" v-bind:src="item.metadata.feature.url">
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
h2.feed {
    text-transform: uppercase;
    color: #505153;
    border-left: 5px solid #fc354c;
    padding: 0px 10px;
    width: 33%;
    clear: both;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
.thumb {
  max-width: 30%;
  float:left;
}
.thumb img {
  margin-bottom: 20px;
}
.desc {
  max-width: 60%;
  float: left;
  padding: 0 15px 40px;
    font-size: 15px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    display: block;
    color: #1b1a1a;
    letter-spacing: -0.2px;
}
small {
  display: block;
}
.time {
  font-family: monospace;
}
.morelink {
  color: #fff;
  text-decoration: none;
  padding: 10px 15px;
  background: #3b3b3b;
  font-size: 12px;
  text-transform: uppercase;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
