<template>
  <header>
    <div class="container flex">
    <img src="../assets/streamflix-logo.png" alt="logo">
    <div class="input">
      <input type="text" class="form-control" placeholder="Cerca un film..">
    </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../style/general.scss";
@import "../style/mixins.scss";;
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
  }
</style>
