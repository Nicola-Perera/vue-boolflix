<template>

  <div id="searchByTitle">
    <header>

      <div id="search">
      <!-- inout dell'utente per cercare film o serie tv -->
      <input type="text" placeholder="search" name="searchByTitle" v-model="title" />
      <button name="search" @click="callApi()">Search</button>

      </div>

    </header>

    <main>

    <div class="search_results">
      <div class="movies">
      <MoviesLayout
        v-model="movies_section"
        v-for="movie in movies"
        :title="movie.title"
        :original_title="movie.original_title"
        :poster="'https://image.tmdb.org/t/p/' + 'w342' + movie.poster_path"
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
        :poster="'https://image.tmdb.org/t/p/' + 'w342' + serie.poster_path"
        :original_language="serie.original_language"
        :vote_average="serie.vote_average"
        :key="serie.id"
      />
      </div>
    </div>

    </main>
  </div>
</template>

<script>
import axios from 'axios'
import MoviesLayout from './MoviesLayout.vue'
import SeriesLayout from './SeriesLayout.vue'

export default {
  name: 'search_results',
  components: {
    MoviesLayout,
    SeriesLayout
  },
  data () {
    return {
      api_key: '8132756f90b9196d3a74d67879dedc3c',
      movies_url: 'https://api.themoviedb.org/3/search/movie',
      series_url: 'https://api.themoviedb.org/3/search/tv',
      poster_base: 'https://image.tmdb.org/t/p/',
      poster_size: 'w342',
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
          `${this.movies_url}?api_key=${this.api_key}&query=${this.title}`
        )
        .then((response) => {
          console.log(response.data.results)
          console.log(this.poster_base)
          console.log(this.poster_size)
          console.log(response.data.results[1].backdrop_path)
          this.movies = response.data.results
        })
        .catch((Error) => {
          console.log(Error, 'ERRORE!')
          this.error = `ERRORE ${Error}`
        })
      axios
        .get(
          `${this.series_url}?api_key=${this.api_key}&query=${this.title}`
        )
        .then((response) => {
          console.log(response.data.results)
          console.log(this.poster_base)
          console.log(this.poster_size)
          console.log(response.data.results[1].backdrop_path)
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
