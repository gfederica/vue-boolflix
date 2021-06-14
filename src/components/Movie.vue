<template>
  <div class="film m-3 p-2">
    <h3>Titolo: {{ item.title }}</h3>
    <h5>Titolo originale: {{ item.original_title }}</h5>
    <h5>Lingua Originale:</h5> 
    <h6 v-if="noFlag">{{ item.original_language }}</h6>
    <h6 v-else><img :src="languageSrc" alt="" class="flag-icon"></h6>
    <h6>Voto: {{ item.vote_average }}</h6>
  </div>
</template>

<script>
export default {
    name: 'Movie',
    props: ["item"],
    data: function() {
        return {
            languageSrc: "",
            noFlag: true
        }
    },
    created: function() {
        const lang = this.item.original_language;
        if (lang == "it") {
            this.languageSrc = require("../assets/it.png"),
            this.noFlag = false
        } else if (lang == "en") {
            this.languageSrc = require("../assets/en.png"),
            this.noFlag = false
        } else {
            this.noFlag = true
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
            width: 50px;
        }
    }
</style>