<template>
<section>
<p>view-source:https://amp2disqus.netlify.com/thisisgentlemen/newsdata/iframe.html</p>
<iframe style="width: 700px; height: 1000px;border: none" src="https://amp2disqus.netlify.com/thisisgentlemen/newsdata/iframe.html">
</iframe>
<p>no idea how to separate them</p>
</section>
</template>



<script>

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
