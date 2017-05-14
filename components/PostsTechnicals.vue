<template>
  <section>
    <div class="">

      <div class=" article">

        <strong>Technical Analysis: All Posts</strong>

        <div v-for="item in this.posts">
          <p>
            <a v-bind:href="item.slug | hash" class="morelink">
              {{item.title}}
            </a>
          </p>
        </div>


        <script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script><ins class="adsbygoogle" style="display:inline-block;width:728px;height:90px" data-ad-client="ca-pub-6979812205705127" data-ad-slot="6506986898"></ins><script>(adsbygoogle = window.adsbygoogle || []).push({});</script>


        <article v-for="item in this.posts">
        <h2 v-bind:id="item.slug" class="feed">
          {{item.title}}
        </h2>
        <p class="time">
          <small v-if="item.created_at">Published: {{item.created_at | moment}}</small>
          <small v-if="item.modified_at">Updated: {{item.modified_at | moment}}</small>
        </p>
        <div v-html="item.content"></div>
       </article>

      </div><!-- // article -->



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
    },
    slug: function (str) {
      return "/ta/"+str
    }
  },
  created () {
    axios.get(`https://api.cosmicjs.com/v1/this-is-g/object-type/technicals`, cache('5 minutes'))
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
.feed {
  width: 100%
}
</style>
