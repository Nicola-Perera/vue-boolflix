<template>
  <div id="MoviesLayout">

    <h2>Titolo del film: {{ title }}</h2>
    <h2>Titolo originale: {{ original_title }}</h2>
    <img :src="poster" :alt="original_title + ' poster'">
    <div class="language">
      <h3>Lingua originale: {{ original_language }}</h3>
      <img :src="require('../assets/img/flags/flag_' + original_language + '.png')" :alt="'Language ' + original_language + ' flag'">
    </div>
    <h3>Valutazione media: {{ vote_average }}</h3>
    <div class="stars_rating">
      {{ stars_rating }}
    </div>

  </div>
</template>

<script>
export default {
  name: 'MoviesLayout',
  props: {
    original_title: String,
    title: String,
    original_language: String,
    poster: String,
    vote_average: Number,
    stars_rating: Function
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
