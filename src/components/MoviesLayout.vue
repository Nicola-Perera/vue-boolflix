<template>
  <div class="movie card">

    <div class="content">

      <!-- media poster -->
      <img v-if="poster != null" :src="poster" :alt="original_title + ' poster'">

      <!-- title -->
      <h2 v-if="title != original_title">Titolo del film: {{ title }}</h2>
      <h2 class="main_title">Titolo originale: {{ original_title }}</h2>

      <!-- language -->
      <div class="language">
        <h3>Lingua originale: {{ original_language }}</h3>
        <img :src="require('../assets/img/flags/flag_' + original_language + '.png')" :alt="'Language ' + original_language + ' flag'">
      </div>

      <!-- rating -->
      <h3>Valutazione media: {{ vote_average }}</h3>

      <div class="stars_rating">
        <span v-for="star in stars_rating" :key="star"> &starf; </span>
        <span v-for="star in (5 - stars_rating)" :key="star"> &star; </span>
      </div>

      <!-- overview -->
      <div v-if="overview != ''">
        <div class="overview">

          <h3>Titolo:</h3>
          <p>{{ original_title }}</p>

          <h3>Voto:</h3>
          <div class="stars_rating">
            <span v-for="star in stars_rating" :key="star"> &starf; </span>
            <span v-for="star in (5 - stars_rating)" :key="star"> &star; </span>
          </div>

          <h3>Overview</h3>
          <p>{{ overview }}</p>

        </div>
      </div>

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
    overview: String,
    vote_average: Number,
    stars_rating: Number
  }
}
</script>

<style lang="scss">
@import "../assets/scss/common_rules.scss";
@import "../assets/scss/card_style.scss";
</style>
