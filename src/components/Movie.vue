<template>
  <div class="film m-3 p-2">
    <h3>{{ item.title }}</h3>
    <h4>{{ item.original_title }}</h4>
    <h4>{{ item.original_language }}</h4>
    <h5>{{ item.vote_average }}</h5>
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