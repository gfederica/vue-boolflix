<template>
  <div class="film m-3 p-2">
    <h3>{{ item.title || item.name }}</h3>
    <h5>Titolo originale: {{ item.original_title || item.original_name }}</h5>
    <h5>Lingua Originale:
        <span v-if="(item.original_language != 'en' && item.original_language != 'it')">{{ item.original_language }}</span>
        <span v-else-if="(item.original_language === 'it')"><img :src="this.language.italian" alt="" class="flag-icon"></span>
        <span  v-else-if="(item.original_language === 'en')"><img :src="this.language.english" alt="" class="flag-icon"></span>
    </h5> 
    <h6>Voto: {{ item.vote_average }}</h6>
  </div>
</template>

<script>
export default {
    name: 'Movie',
    props: ["item"],
    data: function() {
        return {
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
        background-color: $lighterGrey;
        color: $mainText;
        height: 320px;

        .flag-icon {
            max-width: 30px;
            height: 18px;
        }
    }
</style>