<template>
    <div class="container">
        <div class="row p-5">
            <div class="col-6 col-md-4 col-lg-3" v-for="(listItem, index) in list" :key="index">
                <Movie :item="listItem"/>
            </div>
        </div>
    </div>
</template>

<script>
import Movie from './Movie.vue';

export default {
    name: 'Movies',
    props: ["list"],
    components: {
        Movie
    }
}

</script>

<style scoped lang="scss">
@import "../style/general.scss";
@import "../style/mixins.scss";

</style>