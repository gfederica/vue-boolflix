<template>
  <div id="app">
    <Header @performSearch='searchResult'/>
    <main>
      <Movies :list="filteredMovies" :poster="imageUrl"/>
    </main>
  </div>
</template>

<script>

import axios from 'axios';

import Header from './components/Header.vue';
import Movies from './components/Movies.vue';

export default {
  name: 'App',
  components: {
    Header,
    Movies
  },

    data: function() {
        return {
            allMovies: [],
            allSeries: [],
            query: "",
            imageUrl: "https://image.tmdb.org/t/p/w342"
        }
    },
    methods: {
      searchResult: function(input) {
        if (input.trim() == '') {
          this.allMovies = [];
          this.allSeries = [];
        } else if (input.trim() != '') {
          // chiamata film
          axios
         .get ('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: 'aaabb03d86cce59a53d13306abfb0d37',
            query: input,
            language: "it-IT"
        }
        })
         .then (
            (res) => {
                this.allMovies = res.data.results;
            }
        );  
        // chiamata serie
        axios
         .get ('https://api.themoviedb.org/3/search/tv', {
          params: {
            api_key: 'aaabb03d86cce59a53d13306abfb0d37',
            query: input,
            language: "it-IT"
        }
        })
         .then (
            (res) => {
                this.allSeries = res.data.results;
            }
        ); 
        }
      }
    },
    computed: {
      filteredMovies: function() {
        const newArray = [...this.allMovies, ...this.allSeries];
        return newArray;
      }
}
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap';
@import '~@fortawesome/fontawesome-free/css/all.min.css';
@import "./style/general.scss";
@import "./style/mixins.scss";

main {
  background-color: $greyColor ;
}
</style>
