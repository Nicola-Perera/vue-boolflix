<template>
  <!-- componente per l'input dell'utente -->
  <div id="titleSearch">
    <!-- titolo inserito dall'utente -->
    <input type="text" name="searchByTitle" v-model="title" />

    <button name="search" @click="getValue()">Search</button>

    <div class="search_results">
      <CardLayout
        v-model="results"
        v-for="movie in movies"
        :title='movie.title'
        :original_title="movie.original_title"
        :original_language='movie.original_language + " ciao" '
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
      results: '',
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
          // ricevo i risultati della ricerca e li aggiungo alla mia lista
          this.movies = response.data.results

          // alla lista restituita aggiungo la chiave con la bandiera corrispondente alla lingua originale ad ogni oggetto
          this.movies.forEach(element => {
            const languageFlag = {}
            const key = 'flag'
            const value = 'bandiera'
            languageFlag[key] = value
            element.push(languageFlag)
          })
          console.log(this.movies[1].original_language)
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
