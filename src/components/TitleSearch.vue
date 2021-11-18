<template>
  <!-- componente per l'input dell'utente -->
  <div id="titleSearch">
    <!-- titolo inserito dall'utente -->
    <input type="text" name="searchByTitle" v-model="title" />

    <button name="search" @click="getValue()">Search</button>

    <div class="search_results">
      <CardLayout
        v-for="movie in movies"
        :title="movie.title"
        :original_title="movie.original_title"
        :original_language="movie.original_language"
        :vote_average="movie.vote_average"
        :key="movie.id"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import CardLayout from './CardLayout.vue'

export default {
  name: 'titleSearch',
  components: {
    CardLayout
  },
  data () {
    return {
      erroe: '',
      title: '',
      movies: []
    }
  },

  methods: {
    getValue () {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=8132756f90b9196d3a74d67879dedc3c&query=${this.title}`
        )
        .then((response) => {
          this.movies = response.data.results
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
</style>
