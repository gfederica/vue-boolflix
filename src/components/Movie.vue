<template>
  <div class="film">
    <div class="cover">
        <img v-if="item.poster_path != null" :src="`${imageUrl + item.poster_path}`" :alt="(item.title || item.name)">
        <img v-else :src="require('../assets/placeholder.png')" alt="">
        <div class="info">
            <h3>{{ item.title || item.name }}</h3>
            <h6 v-if="this.item.original_title !== this.item.title || this.item.original_name !== this.item.name">Titolo originale: {{ item.original_title || item.original_name }}</h6>
            <h6>Lingua originale:
                <span v-if="(item.original_language != 'en' && item.original_language != 'it')">{{ item.original_language }}</span>
                <span v-else-if="(item.original_language === 'it')"><img :src="this.language.italian" alt="" class="flag-icon"></span>
                <span v-else-if="(item.original_language === 'en')"><img :src="this.language.english" alt="" class="flag-icon"></span>
            </h6> 
            <p>Voto: <i v-for="(star,index) in 5" :key="index" :class="(star <= Math.ceil(item.vote_average / 2))? 'fas fa-star': 'far fa-star'"></i></p>
            <p class="text" v-if="item.overview != ''">{{ item.overview }}</p>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Movie',
    props: ["item"],
    data: function() {
        return {
            imageUrl: "https://image.tmdb.org/t/p/w342",
            star: "",
            language: {
                italian: require("../assets/it.png"),
                english: require("../assets/en.png")
            }
        }
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

        .cover {
            background-color: rgba($color: #000000, $alpha: 0.8);
            height: 457px;
            position: relative;
            
            img:not(.flag-icon) {
                width: 100%;
            }

            &:hover .info {
                opacity: 1;
                cursor: pointer;
            }

            .info {
                background-color: rgba($color: #000000, $alpha: 0.5);
                padding: 10px;
                width: 100%;
                height: 100%;
                position: absolute;
                top: 0;
                left: 0;
                opacity: 0;

                .text {
                height: 50%;
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