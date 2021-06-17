<template>
  <div class="film">
    <div class="cover">
        <img v-if="item.poster_path != null" :src="`${imageUrl + item.poster_path}`" :alt="(item.title || item.name)">
        <img v-else :src="require('../assets/placeholder.png')" alt="">
        <div class="info">
            <h4>{{ item.title || item.name }}</h4>
            <h6 v-if="(this.item.original_title !== this.item.title || this.item.original_name !== this.item.name)">Titolo originale: {{ item.original_title || item.original_name }}</h6>
            <h6>Lingua originale:
                <span v-if="(item.original_language != 'en' && item.original_language != 'it')">{{ item.original_language }}</span>
                <span v-else-if="(item.original_language === 'it')"><img :src="this.language.italian" alt="" class="flag-icon"></span>
                <span v-else-if="(item.original_language === 'en')"><img :src="this.language.english" alt="" class="flag-icon"></span>
            </h6> 
            <p>Voto: <i v-for="(star,index) in 5" :key="index" :class="(star <= Math.ceil(item.vote_average / 2))? 'fas fa-star': 'far fa-star'"></i></p>
            <!-- cast -->
            <div class="cast">
                <h6>Cast:</h6>
                <span v-for="(actor,index) in actors.slice(0, 5)" :key="index">{{actor.name + `, `}}</span>
                <span v-if="actors.length - 1">.</span>
            </div>
            <!-- <div class="genere">
                <h6>Genere:</h6>
                <span v-if="(genres.id.includes(item.genre_ids))">{{genre_ids}}</span>
            </div> -->
            <!-- trama -->
            <p class="text" v-if="item.overview != ''">{{ item.overview }}</p>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'Movie',
    props: ["item"],
    data: function() {
        return {
            imageUrl: "https://image.tmdb.org/t/p/w342",
            language: {
                italian: require("../assets/it.png"),
                english: require("../assets/en.png")
            },
            actors: [],
            moviesGenres: [],
            seriesGenres: [],
            genres: []
        }
    },
    // con created salvo il risultato dei methods, così lascio puliti i data
    created() {
        this.getCast();
        this.getGenre();
    },
    methods: {
        getCast: function() {
            const queryId = this.item.id;
            axios
            .get ( `https://api.themoviedb.org/3/movie/${queryId}/credits`, {
                params: {
                api_key: 'aaabb03d86cce59a53d13306abfb0d37',
                language: "it-IT"
            }
            })
            .then (
                (res) => {
                    if (res.data.cast) {
                        this.actors = res.data.cast
                    }
                }
            )
            .catch((error) => console.log(error));
        },
        getGenre: function() {
            axios
            // chiamata film
            .get ( `https://api.themoviedb.org/3/genre/movie/list`, {
                params: {
                api_key: 'aaabb03d86cce59a53d13306abfb0d37',
                language: "it-IT"
            }
            })
         .then (
            (res) => {
                this.moviesGenres = res.data.genres;
                this.genres = [...this.seriesGenres, ...this.moviesGenres]
            });

            axios
            // chiamata serie
            .get ( `https://api.themoviedb.org/3/genre/tv/list`, {
                params: {
                api_key: 'aaabb03d86cce59a53d13306abfb0d37',
                language: "it-IT"
            }
            })
            .then (
            (res) => {
                this.seriesGenres = res.data.genres;
                this.genres = [...this.seriesGenres, ...this.moviesGenres]
            });
        }
        // ,
        // filterGenre(){
        // return this.genres.filter( (element) =>
        // this.item.genre_ids.includes(element))
        // }
    }
}
</script>

<style scoped lang="scss">
    @import "../style/mixins.scss";
    @import "../style/general.scss";

    .film {
        border: 1px solid white;
        background-color: black;
        background-position: center;
        background-repeat: no-repeat;
        color: $mainText;

        i {
            color: #F7F625;
        }

        h4 {
            color: $mainRed;
        }

        .cover {
            position: relative;
            
            img:not(.flag-icon) {
                width: 100%;
                height: 400px;
            }

            &:hover .info {
                opacity: 1;
                cursor: pointer;
            }

            .info {
                @include flex-column;
                background-color: rgba($color: #000000, $alpha: 0.9);
                padding: 10px;
                width: 100%;
                height: 100%;
                position: absolute;
                top: 0;
                left: 0;
                opacity: 0;

                .cast,
                .genere{
                    font-size: 12px;

                    & h6 {
                        color: $mainRed;
                        font-size: 14px;
                    }
                }

                .text {
                margin-top: 20px;
                font-size: 18px;
                overflow-y: scroll;
                }                
            }
            

        }

        .flag-icon {
            width: 30px;
            height: 18px;
        }
    }
</style>