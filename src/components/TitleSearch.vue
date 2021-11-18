<template>
<!-- componente per l'input dell'utente -->
  <div id="titleSearch">

    <!-- titolo inserito dall'utente -->
    <input type="text" name="searchByTitle" id="searchByTitle">

    <button name="search" @click="findTitle">Search</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'titleSearch',
  data () {
    return {
      erroe: '',
      movies: [],
      findTitle () {
        console.log(this.searchByTitle)
      }
    }
  },

  mounted () {
    axios
      .get('https://api.themoviedb.org/3/search/movie?api_key=8132756f90b9196d3a74d67879dedc3c&query=mad max')
      .then((response) => {
        console.log(this.movies)
        this.movies = response.data.results
        console.log(this.movies)
      })
      .catch((Error) => {
        console.log(Error, 'ERRORE!')
        this.error = `ERRORE ${Error}`
      })
  },
  methods: {
  }
}
</script>

<style lang="scss">
</style>
