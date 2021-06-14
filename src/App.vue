<template>
  <div id="app">
    <Header @performSearch='searchResult'/>
    <main>
      <Movies :list="filteredMovies" :emptySearch="empty"/>
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
            query: "",
            empty: false
        }
    },
    methods: {
      searchResult: function(input) {
        if (input.trim() == '') {
          this.allMovies = [];
          this.empty = true;
        } else if (input.trim() != '') {
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
                console.log(this.allMovies)
            }
        );        
        }
      }
    },
    computed: {
      filteredMovies: function() {
        const newArray = this.allMovies.filter ((element) => {
            return element.title.includes(this.query)
        });
        return newArray;        
      }
}
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap';
@import "./style/general.scss";
@import "./style/mixins.scss";

main {
  background-color: $greyColor ;
}
</style>
