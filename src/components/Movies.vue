<template>
    <div class="container">
        <div class="row p-5" v-if="list.length > 0">
            <div class="col-6 col-md-4 col-lg-3" v-for="(listItem, index) in list" :key="index">
                <Movie :item="listItem" v-bind:style="{ 'background-image': 'url(' + poster + listItem.poster_path + ')' }"/>
            </div>
        </div>
        <div v-else class="alert"><h1>Inserisci il titolo di un film o una serie TV</h1></div>
    </div>
</template>

<script>
import Movie from './Movie.vue';

export default {
    name: 'Movies',
    props: ["list", "poster"],
    components: {
        Movie
    }
}

</script>

<style scoped lang="scss">
@import "../style/general.scss";
@import "../style/mixins.scss";

.container {
    min-height: 90vh;

    .alert {
        @include flex;
        height: 100%;
        color: $lighterGrey;
    }
}

</style>