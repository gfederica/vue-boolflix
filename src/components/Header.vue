<template>
  <header>
    <div class="container flex">
      <img src="../assets/streamflix-logo.png" alt="logo">
      <form class="flex">
        <div class="input">
          <input type="text" class="form-control" placeholder="Cerca un film.." v-model.trim="searchMovie"
              @keyup="$emit('performSearch', searchMovie)">
            
              
              
        </div>
        <button type="submit" class="btn btn-primary m-2" @click.prevent="$emit('performSearch', searchMovie)">Cerca</button>
      </form>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data: function() {
      return {
          searchMovie: ""
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../style/general.scss";
@import "../style/mixins.scss";
  header {
    background-color: black;

      .flex {
        @include flex;
        justify-content: space-between;
        height: 10vh;
      }

      img {
        height: 50px;
      }

      .btn {
        background-color: $mainRed;
        border: 1px solid $mainRed;
      }
  }
</style>
