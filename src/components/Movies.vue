<template>
    <div class="container">
        <div class="row p-5">
            <div class="col-6 col-md-4 col-lg-3" v-for="(movie, index) in movies" :key="index">
                <Movie :item="movie"/>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import Movie from './Movie.vue';

export default {
    name: 'Movies',
    components: {
        Movie
    },
    data: function() {
        return {
            movies: [],
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
                this.movies = res.data.results;
                console.log(this.movies);
            }
        );
    }
}

</script>

<style scoped lang="scss">
@import "../style/general.scss";
@import "../style/mixins.scss";

</style>