<template>
  <!-- BOOLFLIX -->
  <!-- sito di distribuzione di film e serie tv -->
  <div id="app">

    <main>

      <!-- search by title section -->
      <div id="search">
        <TitleSearch />
      </div>

    </main>

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
  @import "./assets/scss/common_rules.scss";
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;700&display=swap');

body {
  background-color: var(--primary-color);
}
  #app {
    background-color: var(--primary-color);
  }

</style>
