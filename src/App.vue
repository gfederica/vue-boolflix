<template>
  <div id="app">
    <Header/>
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    Header
  },
  data: function() {
    return {
        query: "prova"
    }
},
  created: function() {
    axios
    .get ('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: 'aaabb03d86cce59a53d13306abfb0d37',
        query: this.query,
        language: "it-IT"
      }
    })
    .then (
        (res) => {
            console.log(res);
        }
    );
  }
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap';
</style>
