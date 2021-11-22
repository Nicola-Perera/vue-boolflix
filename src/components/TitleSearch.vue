<template>

  <div id="searchByTitle">
    <header>

      <div id="logo">
        <img src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="Netflix logo">
      </div>

      <div class="inputs">
      <!-- input dell'utente per cercare film o serie tv -->
      <input id="search_input" type="text" placeholder="Search for a title" name="searchByTitle" v-model="title" />
      <button id="search_button" name="search" @click="callApi()">GO</button>

      </div>

    </header>

    <main>

      <div id="genres" class="container">
        <div v-for="genre in genres" :key="genre.id">
          <h2>{{ genre.name }}</h2>
        </div>
      </div>

    <div class="search_results container">
      <div class="movies container">
      <MoviesLayout
        v-model="movies_section"
        v-for="movie in movies"
        :title="movie.title"
        :original_title="movie.original_title"
        :poster="'https://image.tmdb.org/t/p/' + 'w342' + movie.poster_path"
        :original_language="movie.original_language"
        :vote_average="movie.vote_average"
        :stars_rating="fiveStars(movie.vote_average)"
        :overview="movie.overview"
        :key="movie.id"
      />
      </div>

      <div class="series container">
      <SeriesLayout
        v-model="series_section"
        v-for="serie in series"
        :name="serie.title"
        :original_name="serie.original_name"
        :poster="'https://image.tmdb.org/t/p/' + 'w342' + serie.poster_path"
        :original_language="serie.original_language"
        :vote_average="serie.vote_average"
        :stars_rating="fiveStars(serie.vote_average)"
        :overview="serie.overview"
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
      series: [],
      genres: [{ id: 28, name: 'Action' }, { id: 12, name: 'Adventure' }, { id: 16, name: 'Animation' }, { id: 35, name: 'Comedy' }, { id: 80, name: 'Crime' }, { id: 99, name: 'Documentary' }, { id: 18, name: 'Drama' }, { id: 10751, name: 'Family' }, { id: 14, name: 'Fantasy' }, { id: 36, name: 'History' }, { id: 27, name: 'Horror' }, { id: 10402, name: 'Music' }, { id: 9648, name: 'Mystery' }, { id: 10749, name: 'Romance' }, { id: 878, name: 'Science Fiction' }, { id: 10770, name: 'TV Movie' }, { id: 53, name: 'Thriller' }, { id: 10752, name: 'War' }, { id: 37, name: 'Western' }]
    }
  },

  methods: {
    callApi () {
      // Movies API
      axios
        .get(
          `${this.movies_url}?api_key=${this.api_key}&query=${this.title}`
        )
        .then((response) => {
          console.log(response.data.results)
          this.movies = response.data.results
        })
        .catch((Error) => {
          console.log(Error, 'ERRORE!')
          this.error = `ERRORE ${Error}`
        })

      // TV Series API
      axios
        .get(
          `${this.series_url}?api_key=${this.api_key}&query=${this.title}`
        )
        .then((response) => {
          console.log(response.data.results)
          this.series = response.data.results
        })
        .catch((Error) => {
          console.log(Error, 'ERRORE!')
          this.error = `ERRORE ${Error}`
        })
    },
    // stars-rating function
    fiveStars (vote) {
      return Number((vote / 2).toFixed())
    }
  }
}

</script>

<style lang="scss">
.search_results {
  display: flex;
  justify-content: space-between
}
  @import "../assets/scss/common_rules.scss";
  // @import "../assets/scss/genres_filter.scss";
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;700&display=swap');

// header rules
  header {
    width: 100%;
    padding: 1rem 3rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    // position: fixed;
    background-color: var(--secondary-color);

    #logo {
      height: 50px;

      img {
        height: 100%;
      }
    }

      // search title
    .inputs {
      font-family: inherit;

      #search_input {
        &::placeholder {
          color: #7378c5;
        }
        &:focus {
          outline: 0;
          background-color: var(--primary-color);
        }

        background-color: transparent;
        border: 2px solid var(--primary-color);
        border-radius: 2rem;
        padding: .5rem 1rem;
        margin-right: 1rem;
        font-size: 1rem;
        color: #fff;
      }

      #search_button {
        background-color: var(--send-input-color);
        border-radius: 2rem;
        padding: .5rem;
      }
    }
  }

  // main
  main {

    // genres filter
    #genres {
      justify-content: center;
      flex-wrap: wrap;
    }
    // cards container
    .search_results {
      padding: 3rem;

    }
  }
</style>
