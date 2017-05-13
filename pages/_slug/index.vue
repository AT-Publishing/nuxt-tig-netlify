<template>
  <section class="container">

    <div class="side">
      <my-bar />
    </div>

    <h1 class="article">{{ object.title }}</h1>
    <p class="time article">
      <small v-if="object.created_at">
        <time v-bind:datetime="object.created_at">Published: {{object.created_at | moment}}</time>
      </small>
      <small v-if="object.modified_at">
        <time v-bind:datetime="object.modified_at">Updated: {{object.modified_at | moment}}</time>
      </small>
      <small>
        Author: <a target="_blank" href="https://reddit.com/u/_this_is_gentlemen">Reddit</a>
      </small>
      <small v-if="object.metadata.description">
        Short: <span v-html="object.metadata.description"></span>
      </small>
    </p>

    <div class="article">

      <div v-if="object.metadata.feature" class="feature">
        <img v-bind:src="object.metadata.feature.url">
      </div>

      <div v-html="object.content" ></div>

    </div>


  </section>
</template>

<script>
import axios from 'axios'
import moment from 'moment'
import MyBar from '~components/Bar.vue'
export default {
  validate ({ params }) {
    return params
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
    }
  },
  asyncData ({ params, error }) {
    console.log(params)
    return axios.get(`https://api.cosmicjs.com/v1/this-is-g/object/${params.slug}`)
    .then((res) => res.data)
    .catch(() => {
      error({ message: 'Page router says not found, m8. Houboudat?', statusCode: 404 })
    })
  },
  head () {
    return {
      title: `${this.object.title} | This Is Gentlemen `
    }
  }
}
</script>

<style scoped>
.article {
  width: 65%;
  text-align: left;
  margin: 0px;
  box-sizing: border-box;
  padding: 0 25px;
  position: relative;
  float: left;
  margin-bottom: 10px 
}
h1 {
  width: 65%;
  text-align: left;
  text-transform: uppercase;
  color: #505153;
  border-bottom: 5px solid #fc354c;
  padding-left: 0 !important;
  font-size: 36px;
  font-weight: 500;
  margin-left:25px !important;
  margin-bottom: 10px !important;
}
.feature {
  max-width: 100%;
}
</style>
