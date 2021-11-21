<template>
  <div id="MoviesLayout">

    <!-- title -->
    <h2>Titolo del film: {{ title }}</h2>
    <h2>Titolo originale: {{ original_title }}</h2>
    <img :src="poster" :alt="original_title + ' poster'">

    <!-- language -->
    <div class="language">
      <h3>Lingua originale: {{ original_language }}</h3>
      <img :src="require('../assets/img/flags/flag_' + original_language + '.png')" :alt="'Language ' + original_language + ' flag'">
    </div>

    <!-- rating -->
    <h3>Valutazione media: {{ vote_average }}</h3>

    <div class="stars_rating">
      <span v-for="star in fullStars" :key="star"> &starf; </span>
      <span v-for="star in emptyStars" :key="star"> &star; </span>
    </div>

  </div>
</template>

<script>
export default {
  name: 'MoviesLayout',
  data () {
    return {
      fullStars: '',
      emptyStars: ''
    }
  },
  props: {
    original_title: String,
    title: String,
    original_language: String,
    poster: String,
    vote_average: Number,
    stars_rating: Number
  },
  mounted () {
    console.log('movie')
    console.log(this.stars_rating)
    this.fullStars = this.stars_rating
    this.emptyStars = 5 - this.fullStars
    this.fullStars = 5 - this.emptyStars
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
