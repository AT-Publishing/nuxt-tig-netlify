<!-- component template -->
<script type="text/x-template" id="grid-template">
  <table>
    <thead>
      <tr>
        <th v-for="key in columns"
          @click="sortBy(key)"
          :class="{ active: sortKey == key }">
          {{ key | capitalize }}
          <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'">
          </span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="entry in filteredData">
        <td v-for="key in columns">
          {{entry[key] | moment }}
        </td>
      </tr>
    </tbody>
  </table>
</script>

<section>
  <div class="datablock">

    <h3>LATEST</h3>
    <!-- latest -->

    <div id="ft">
      <h4>ft / latest</h4>
      <p><button v-on:click="getData">LOAD</button></p>
      <p><form id="search">
        Search <input name="query" v-model="searchQuery">
      </form></p>
      <demo-grid
        :data="gridData"
        :columns="gridColumns"
        :filter-key="searchQuery">
      </demo-grid>
    </div>

    <div id="bi">
      <h4>business insider / latest</h4>
      <p><button v-on:click="getData">LOAD</button></p>
      <p><form id="search">
        Search <input name="query" v-model="searchQuery">
      </form></p>
      <demo-grid
        :data="gridData"
        :columns="gridColumns"
        :filter-key="searchQuery">
      </demo-grid>
    </div>

    <div id="hb">
      <h4>handelsblatt / latest</h4>
      <p><button v-on:click="getData">LOAD</button></p>
      <p><form id="search">
        Search <input name="query" v-model="searchQuery">
      </form></p>
      <demo-grid
        :data="gridData"
        :columns="gridColumns"
        :filter-key="searchQuery">
      </demo-grid>
    </div>

  </div>
</section>


<section>
  <div class="datablock">

    <h3>TOP</h3>
    <!-- top -->

    <div id="bloomberg">
      <h4>bloomberg / top</h4>
      <p><button v-on:click="getData">LOAD</button></p>
      <p><form id="search">
        Search <input name="query" v-model="searchQuery">
      </form></p>
      <demo-grid
        :data="gridData"
        :columns="gridColumns"
        :filter-key="searchQuery">
      </demo-grid>
    </div>

    <div id="cnbc">
      <h4>cnbc / top</h4>
      <p><button v-on:click="getData">LOAD</button></p>
      <p><form id="search">
        Search <input name="query" v-model="searchQuery">
      </form></p>
      <demo-grid
        :data="gridData"
        :columns="gridColumns"
        :filter-key="searchQuery">
      </demo-grid>
    </div>

    <div id="wsj">
      <h4>wsj / top</h4>
      <p><button v-on:click="getData">LOAD</button></p>
      <p><form id="search">
        Search <input name="query" v-model="searchQuery">
      </form></p>
      <demo-grid
        :data="gridData"
        :columns="gridColumns"
        :filter-key="searchQuery">
      </demo-grid>
    </div>

  </div>
</section>




<script type="text/javascript">

import Vue from 'vue'
import _ from 'lodash'
import moment from 'moment'

Vue.component('demo-grid', {
template: '#grid-template',
props: {
  data: Array,
  columns: Array,
  filterKey: String
},
data: function () {
  var sortOrders = {}
  this.columns.forEach(function (key) {
    sortOrders[key] = 1
  })
  return {
    sortKey: '',
    sortOrders: sortOrders
  }
},
computed: {
  filteredData: function () {
    var sortKey = this.sortKey
    var filterKey = this.filterKey && this.filterKey.toLowerCase()
    var order = this.sortOrders[sortKey] || 1
    var data = this.data
    if (filterKey) {
      data = data.filter(function (row) {
        return Object.keys(row).some(function (key) {
          return String(row[key]).toLowerCase().indexOf(filterKey) > -1
        })
      })
    }
    if (sortKey) {
      data = data.slice().sort(function (a, b) {
        a = a[sortKey]
        b = b[sortKey]
        return (a === b ? 0 : a > b ? 1 : -1) * order
      })
    }
    return data
  }
},
filters: {
  capitalize: function (str) {
    return str.charAt(0).toUpperCase() + str.slice(1)
  },
  moment: function(str) {
    var d = new Date(str);
    if (moment(d).isValid() ) {
      return moment(d).format('MMMM Do \'YY, h:mm a');
    } else {
      return str;
    }
  }
},
methods: {
  sortBy: function (key) {
    this.sortKey = key
    this.sortOrders[key] = this.sortOrders[key] * -1
  }
}
})

// bootstrap the bloomberg
var bloomberg = new Vue({
el: '#bloomberg',
methods: {
  getData: _.debounce(
    function () {
      var vm = this
      axios.get('https://newsapi.org/v1/articles?source=bloomberg&sortBy=top&apiKey=ae1193384a944116895698c121153073')
        .then(function (response) {
          vm.gridData = response.data.articles
        })
        .catch(function (error) {
          vm.gridData = 'Error! Could not reach the API. ' + error
        })
    },
    100
  )
},
data: {
  searchQuery: '',
  gridColumns: ['title', 'description', 'publishedAt', 'url'],
  gridData: [
  {
    "author": "-",
    "title": "-",
    "description": "-",
    "url": "-",
    "urlToImage": "-",
    "publishedAt": "-"
  }
  ]
}
})

// financial times
var ft = new Vue({
el: '#ft',
methods: {
  getData: _.debounce(
    function () {
      var vm = this
      axios.get('https://newsapi.org/v1/articles?source=financial-times&sortBy=latest&apiKey=ae1193384a944116895698c121153073')
        .then(function (response) {
          vm.gridData = response.data.articles
        })
        .catch(function (error) {
          vm.gridData = 'Error! Could not reach the API. ' + error
        })
    },
    100
  )
},
data: {
  searchQuery: '',
  gridColumns: ['title', 'description', 'publishedAt', 'url'],
  gridData: [
  {
    "author": "-",
    "title": "-",
    "description": "-",
    "url": "-",
    "urlToImage": "-",
    "publishedAt": "-"
  }
  ]
}
})

// cnbc
var cnbc = new Vue({
el: '#cnbc',
methods: {
  getData: _.debounce(
    function () {
      var vm = this
      axios.get('https://newsapi.org/v1/articles?source=cnbc&sortBy=top&apiKey=ae1193384a944116895698c121153073')
        .then(function (response) {
          vm.gridData = response.data.articles
        })
        .catch(function (error) {
          vm.gridData = 'Error! Could not reach the API. ' + error
        })
    },
    100
  )
},
data: {
  searchQuery: '',
  gridColumns: ['title', 'description', 'publishedAt', 'url'],
  gridData: [
  {
    "author": "-",
    "title": "-",
    "description": "-",
    "url": "-",
    "urlToImage": "-",
    "publishedAt": "-"
  }
  ]
}
})

// wsj
var wsj = new Vue({
el: '#wsj',
methods: {
  getData: _.debounce(
    function () {
      var vm = this
      axios.get('https://newsapi.org/v1/articles?source=the-wall-street-journal&sortBy=top&apiKey=ae1193384a944116895698c121153073')
        .then(function (response) {
          vm.gridData = response.data.articles
        })
        .catch(function (error) {
          vm.gridData = 'Error! Could not reach the API. ' + error
        })
    },
    100
  )
},
data: {
  searchQuery: '',
  gridColumns: ['title', 'description', 'publishedAt', 'url'],
  gridData: [
  {
    "author": "-",
    "title": "-",
    "description": "-",
    "url": "-",
    "urlToImage": "-",
    "publishedAt": "-"
  }
  ]
}
})


// hb
var hb = new Vue({
el: '#hb',
methods: {
  getData: _.debounce(
    function () {
      var vm = this
      axios.get('https://newsapi.org/v1/articles?source=handelsblatt&sortBy=latest&apiKey=ae1193384a944116895698c121153073')
        .then(function (response) {
          vm.gridData = response.data.articles
        })
        .catch(function (error) {
          vm.gridData = 'Error! Could not reach the API. ' + error
        })
    },
    100
  )
},
data: {
  searchQuery: '',
  gridColumns: ['title', 'description', 'publishedAt', 'url'],
  gridData: [
  {
    "author": "-",
    "title": "-",
    "description": "-",
    "url": "-",
    "urlToImage": "-",
    "publishedAt": "-"
  }
  ]
}
})


// bi
var bi = new Vue({
el: '#bi',
methods: {
  getData: _.debounce(
    function () {
      var vm = this
      axios.get('https://newsapi.org/v1/articles?source=business-insider&sortBy=latest&apiKey=ae1193384a944116895698c121153073')
        .then(function (response) {
          vm.gridData = response.data.articles
        })
        .catch(function (error) {
          vm.gridData = 'Error! Could not reach the API. ' + error
        })
    },
    100
  )
},
data: {
  searchQuery: '',
  gridColumns: ['title', 'description', 'publishedAt', 'url'],
  gridData: [
  {
    "author": "-",
    "title": "-",
    "description": "-",
    "url": "-",
    "urlToImage": "-",
    "publishedAt": "-"
  }
  ]
}
})
</script>



<style scoped>
          body {
          font-family: 'Raleway', sans-serif;
          font-size: 11px;
          color: inherit;
          }

        section > .datablock {
          display: block;
          background: rgba(160, 160, 160, 0.075);
          padding: 30px;
          margin-bottom: 30px;
          border-radius: 10px;
        }

        section > .datablock > div {
            background-repeat: no-repeat!important;
            background-position: right top!important;
        }
          section > .datablock > div#ft {
            background: url(../assets/img/news/ft.png);
          }
          section > .datablock > div#cnbc {
            background: url(../assets/img/news/cnbc.png);
          }
          section > .datablock > div#bloomberg {
            background: url(../assets/img/news/bloomberg.png);
          }
          section > .datablock > div#hb {
            background: url(../assets/img/news/hb.png);
          }
          section > .datablock > div#bi {
            background: url(../assets/img/news/bi.png);
          }
          section > .datablock > div#wsj {
            background: url(../assets/img/news/wsj.png);
          }

        table {
        border: none;
        border-collapse: collapse;
        font-family: "Source Sans Pro";
        text-rendering: optimizeSpeed;
        }

        th {
        cursor: pointer;
        -webkit-user-select: none;
        -moz-user-select: none;
        -user-select: none;
        }


        th, td {
        display: table-cell;
        padding: 10px 20px;
        }

        th.active {
        color: #111;
        }

        th.active .arrow {
        opacity: 1;
        }
        table tbody tr {
          background-color: #fff;
        }
        table tbody tr:nth-child(2n + 1) {
        background-color: rgba(160, 160, 160, 0.075);
        }
        table th {
            color: #3c3b3b;
            font-size: 11px;
            font-weight: 700;
            padding: 0 0.75em 0.75em 0.75em;
            text-align: left;
            text-transform: uppercase;
        }
        table td {
          font-size: 11px;
          border-bottom: 1px solid #aaa;
          padding: 0.75em 0.75em;
        }

        .arrow {
        display: inline-block;
        vertical-align: middle;
        width: 0;
        height: 0;
        margin-left: 5px;
        opacity: 0.66;
        }

        .arrow.asc {
        border-left: 4px solid transparent;
        border-right: 4px solid transparent;
        border-bottom: 4px solid #fff;
        }

        .arrow.dsc {
        border-left: 4px solid transparent;
        border-right: 4px solid transparent;
        border-top: 4px solid #fff;
        }

        #search {
        margin-bottom: 10px;
        }

        .highlight {
          background-color: yellow;
        }

        @media (max-width: 480px) {

            table td, table th {
              display: block;
            }
            section > .datablock > div {
              background-size: 60px!important;
            }
            input {
              width: 100%;
            }


        }
</style>
