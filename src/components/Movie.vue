<template>
  <div class="film m-3 p-2">
    <h3>Titolo: {{ item.title }}</h3>
    <h5>Titolo originale: {{ item.original_title }}</h5>
    <h5>Lingua Originale: {{ item.original_language }}</h5>
    <h6>Voto: {{ item.vote_average }}</h6>
  </div>
</template>

<script>
export default {
    name: 'Movie',
    props: ["item"]
}
</script>

<style scoped lang="scss">
    @import "../style/mixins.scss";
    @import "../style/general.scss";
    .film {
        background-color: $lighterGrey;
        color: $mainText;
        height: 320px;
    }
</style>