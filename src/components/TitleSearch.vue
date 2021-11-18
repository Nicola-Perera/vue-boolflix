<template>
  <div id="titleSearch">
    <input type="text" name="searchByTitle">
    <button name="search">Search</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'titleSearch',
  data () {
    return {
      erroe: '',
      movies: []
    }
  },

  mounted () {
    axios
      .get('https://api.themoviedb.org/3/search/movie?api_key=8132756f90b9196d3a74d67879dedc3c&query=avatar')
      .then((response) => {
        console.log(this.movies)
        this.movies = response.data.results
        console.log(this.movies.)
      })
      .catch((Error) => {
        console.log(Error, 'ERRORE!')
        this.error = `ERRORE ${Error}`
      })
  }
}
</script>

<style lang="scss">
</style>
