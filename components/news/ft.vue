<template>
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
</template>

<script>

</script>
