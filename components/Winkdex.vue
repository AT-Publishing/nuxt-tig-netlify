<template>
  <div id="winkdex">
    Winkdex: $ {{ $data.gridData.price | dollars }}
  </div>
</template>

<script>
import moment from 'moment'
import axios from 'axios'
import apicache from 'apicache'

let cache = apicache.middleware

export default {
      data () {
        return {
          gridData: [
            {
              "price": "-",
              "timestamp": "-"
            }
          ]
        }
      },
      filters: {
        dollars: function(str) {
          var dp = str/100
          if (isNaN(dp)) {
            return "-"
          } else {
            return dp
          }
        }
      },
      created () {
        axios.get(`https://thisisgentlemen.net/winkdex/response.json`, cache('30 seconds'))
        .then(response => {
          this.gridData = response.data
        })
        setInterval(function() {
          axios.get(`https://thisisgentlemen.net/winkdex/response.json`, cache('30 seconds'))
          .then(response => {
            this.gridData = response.data
          })
        }, 30000)
      }
}
</script>

<style scoped>
#winkdex {
  color: #fff;
  text-transform: uppercase;
}
</style>
