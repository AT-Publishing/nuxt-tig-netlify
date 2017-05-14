<template>
  <section>
    <div class="">

      <div class="side">

        <h4>Technical Analysis: All Posts</h4>

        <div v-for="item in this.posts">
          <p>
            <a v-bind:href="item.slug | hash" class="morelink">
              {{item.title}}
            </a>
          </p>
        </div>

        <my-bar />

      </div>


      <div class=" article">



        <ins class="adsbygoogle" style="display:inline-block;width:728px;height:90px" data-ad-client="ca-pub-6979812205705127" data-ad-slot="6506986898"></ins><script>(adsbygoogle = window.adsbygoogle || []).push({});</script>


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


      <div class="aside">

        <!-- tig_sky -->
        <ins class="adsbygoogle"
             style="display:inline-block;width:160px;height:600px"
             data-ad-client="ca-pub-6979812205705127"
             data-ad-slot="7061619693"></ins>
        <script>
        (adsbygoogle = window.adsbygoogle || []).push({});
        </script>

      </div>



    </div>
  </section>
</template>

<script>
import moment from 'moment'
import axios from 'axios'
import apicache from 'apicache'
import MyBar from '~components/Bar.vue'

let cache = apicache.middleware
export default {
  name: 'home',
  data () {
    return {
      posts: []
    }
  },
  components: {
    MyBar
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
  max-width: 55%;
  margin: 0;
  text-align: left;
  float: left;
}
.feed {
  width: 100%
}
.aside {
  max-width: 15%;
  margin: 0 auto;
  text-align: center;
  float: left;
}
.aside * {
  margin: 0 auto
}
@media (max-width: 776px) {
  .aside {
    display: none;
  }
}
</style>
