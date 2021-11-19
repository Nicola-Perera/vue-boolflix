<template>
  <div id="SeriesLayout">

    <h2>Nome della serie: {{ name }}</h2>
    <h2>Nome originale: {{ original_name }}</h2>
    <div class="language">
      <h3>Lingua originale: {{ original_Language }}</h3>
      <img :src="require('../assets/img/flags/flag_' + original_language + '.png')" :alt="'Language ' + original_language + ' flag'">
    </div>
    <h3>Valutazione media: {{ vote_average }}</h3>
  </div>
</template>

<script>
export default {
  name: 'SeriesLayout',
  props: {
    original_name: String,
    name: String,
    original_language: String,
    vote_average: Number
  }
}
</script>

<style lang="scss">
.language {
  width: 5%;
  img {
    width: 100%;
  }
}
</style>
