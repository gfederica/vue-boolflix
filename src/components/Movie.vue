<template>
  <div class="film m-3 p-2">
    <h3>{{ item.title || item.name }}</h3>
    <h5>Titolo originale: {{ item.original_title || item.original_name }}</h5>
    <h5>Lingua Originale:
        <span v-if="(item.original_language != 'en' && item.original_language != 'it')">{{ item.original_language }}</span>
        <span v-else-if="(item.original_language === 'it')"><img :src="this.language.italian" alt="" class="flag-icon"></span>
        <span  v-else-if="(item.original_language === 'en')"><img :src="this.language.english" alt="" class="flag-icon"></span>
    </h5> 
    <h6>Voto: <i v-for="(star,index) in 5" :key="index" :class="(star <= Math.ceil(item.vote_average / 2))? 'fas fa-star': 'far fa-star'"></i></h6>
  </div>
</template>

<script>
export default {
    name: 'Movie',
    props: ["item"],
    data: function() {
        return {
            star: ""
        }
    }
}
</script>

<style scoped lang="scss">
    @import "../style/mixins.scss";
    @import "../style/general.scss";
    .film {
        background-color: black;
        background-position: center;
        background-size: 85%;
        background-repeat: no-repeat;
        
        color: $mainText;
        height: 320px;

        .flag-icon {
            max-width: 30px;
            height: 18px;
        }
    }
</style>