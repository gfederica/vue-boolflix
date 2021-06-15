<template>
  <div class="film m-3">
    <div class="cover p-2">
        <h3>{{ item.title || item.name }}</h3>
        <h6>Titolo originale: {{ item.original_title || item.original_name }}</h6>
        <h6>Lingua originale:
            <span v-if="(item.original_language != 'en' && item.original_language != 'it')">{{ item.original_language }}</span>
            <span v-else-if="(item.original_language === 'it')"><img :src="this.language.italian" alt="" class="flag-icon"></span>
            <span  v-else-if="(item.original_language === 'en')"><img :src="this.language.english" alt="" class="flag-icon"></span>
        </h6> 
        <p>Voto: <i v-for="(star,index) in 5" :key="index" :class="(star <= Math.ceil(item.vote_average / 2))? 'fas fa-star': 'far fa-star'"></i></p>
        <p class="text" v-if="item.overview != ''">{{ item.overview }}</p>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Movie',
    props: ["item"],
    data: function() {
        return {
            star: "",
            languageSrc: "",
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
        width: 342px;
        height: 457px;

        i {
            color: #F7F625;
        }

        .cover {
            background-color: rgba($color: #000000, $alpha: 0.8);
            height: 100%;
            width: 100%;
            opacity: 0;

            &:hover {
                opacity: 1;
            }

            .text {
                height: 280px;
                font-size: 18px;
                overflow-y: scroll;
            }
        }

        .flag-icon {
            width: 30px;
            height: 18px;
        }
    }
</style>