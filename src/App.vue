<template>
  <!-- BOOLFLIX -->
  <!-- sito di distribuzione di film e serie tv -->
  <div id="app">

    <!-- input per cercare un film tramite titolo -->
    <TitleSearch />
  </div>
</template>

<script>
import TitleSearch from './components/TitleSearch.vue'

export default {
  components: {
    TitleSearch
  }
}
</script>

<style lang="scss">
</style>
