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
        :original_language='movie.original_language'
        :vote_average="movie.vote_average"
        :flag="movie.flag"
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
            // abbino alle principali lingue le loro bandiere
            if (element.original_language === 'en') {
              console.log('english')
            } else if (element.original_language === 'fr') {
              console.log('french')
            } else if (element.original_language === 'de') {
              console.log('german')
            } else if (element.original_language === 'it') {
              console.log('italian')
            } else if (element.original_language === 'pt') {
              console.log('portuguese')
            } else if (element.original_language === 'ru') {
              console.log('russian')
            } else if (element.original_language === 'es') {
              console.log('spanish')
            } else if (element.original_language === 'da') {
              console.log('danish')
            } else {
              console.log('no flag')
            }
            element.flag = `https://www.google.it/search?q=bandiera+${element.original_language}&hl=it&authuser=0&tbm=isch&source=hp&biw=1280&bih=721&ei=lJCXYbmnBseNxc8P9IGQyAI&iflsig=ALs-wAMAAAAAYZeepBlcPPvtsVjqyfDUIUS0Rel06cOr&ved=0ahUKEwi5wd-Or6T0AhXHRvEDHfQABCkQ4dUDCAY&uact=5&oq=bandiera+it&gs_lcp=CgNpbWcQAzIICAAQgAQQsQMyCAgAEIAEELEDMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQ6CwgAEIAEELEDEIMBOggIABCxAxCDAToECAAQA1DvBFjOFWC8GGgBcAB4AIABdogBvwaSAQQxMC4xmAEAoAEBqgELZ3dzLXdpei1pbWewAQA&sclient=img#imgrc=UfE7dDLh2BqBfM`
          })
          // console.log(this.movies[1].original_language)
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
