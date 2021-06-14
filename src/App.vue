<template>
  <div id="app">
    <Header/>
    <main>
      <Movies/>
    </main>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Movies from './components/Movies.vue';

export default {
  name: 'App',
  components: {
    Header,
    Movies
  }
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap';
@import "./style/general.scss";
@import "./style/mixins.scss";

main {
  background-color: $greyColor ;
}
</style>
