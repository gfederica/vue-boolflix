<template>
    <div class="container">
        <section v-if="movieList.length > 0">
            <h2>Film</h2>
            <div class="row row-cols-4">
            <div class="cinema" v-for="(listItem, index) in movieList" :key="index">
                <Movie :item="listItem" :style="{'background-image': 'url(' + poster + listItem.poster_path + ')'}"/>
            </div>
        </div>
        </section>
        <section v-if="seriesList.length > 0">
            <h2>Serie TV</h2>
            <div class="row row-cols-4">
            <div class="series" v-for="(listItem, index) in seriesList" :key="index">
                <Movie :item="listItem" :style="{'background-image': 'url(' + poster + listItem.poster_path + ')'}"/>
            </div>
        </div>
        </section>
        
        <div v-if="movieList.length == 0 && seriesList.length == 0 && !searching" class="alert"><h1>Inserisci il titolo di un film o una serie TV</h1></div>
    </div>
</template>

<script>
import Movie from './Movie.vue';

export default {
    name: 'Movies',
    props: ["movieList","seriesList","poster"],
    components: {
        Movie
    },
    methods: {
        getBackground: function() {
            console.log(this.list.poster_path);
        }
    }
}

</script>

<style scoped lang="scss">
@import "../style/general.scss";
@import "../style/mixins.scss";

h2 {
    color: $mainText;
    padding-top: 30px;
}

.cinema, .series {
    margin-bottom: 15px;
}

.container {
    min-height: 90vh;

    .alert {
        @include flex;
        height: 100%;
        color: $lighterGrey;
    }
}

</style>