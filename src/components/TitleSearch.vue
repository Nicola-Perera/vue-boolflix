<template>
  <!-- componente per l'input dell'utente -->
  <div id="titleSearch">
    <!-- titolo inserito dall'utente -->
    <input type="text" name="searchByTitle" v-model="title" />

    <button name="search" @click="callApi()">Search</button>

    <div class="search_results">
      <div class="movies">
      <MoviesLayout
        v-model="movies_section"
        v-for="movie in movies"
        :title="movie.title"
        :original_title="movie.original_title"
        :original_language="movie.original_language"
        :vote_average="movie.vote_average"
        :key="movie.id"
      />
      </div>

      <div class="series">
      <SeriesLayout
        v-model="series_section"
        v-for="serie in series"
        :name="serie.title"
        :original_name="serie.original_name"
        :original_language="serie.original_language"
        :vote_average="serie.vote_average"
        :key="serie.id"
      />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import MoviesLayout from './MoviesLayout.vue'
import SeriesLayout from './SeriesLayout.vue'

export default {
  name: 'titleSearch',
  components: {
    MoviesLayout,
    SeriesLayout
  },
  data () {
    return {
      api_key: '8132756f90b9196d3a74d67879dedc3c',
      movies_url: 'https://api.themoviedb.org/3/search/movie',
      errore: '',
      title: '',
      movies_section: '',
      series_section: '',
      languages_available: ['it', 'en', 'de', 'fr', 'es', 'ru'],
      movies: [],
      series: []
    }
  },

  methods: {
    callApi () {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=8132756f90b9196d3a74d67879dedc3c&query=${this.title}`
        )
        .then((response) => {
          console.log(response.data.results)
          this.movies = response.data.results
        })
        .catch((Error) => {
          console.log(Error, 'ERRORE!')
          this.error = `ERRORE ${Error}`
        })
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=8132756f90b9196d3a74d67879dedc3c&language=en-US&page=1&query=${this.title}`
        )
        .then((response) => {
          console.log(response.data.results)
          this.series = response.data.results
        })
        .catch((Error) => {
          console.log(Error, 'ERRORE!')
          this.error = `ERRORE ${Error}`
        })
    }
  }
}

</script>

<style lang="scss">
.search_results {
  display: flex;
}
</style>
