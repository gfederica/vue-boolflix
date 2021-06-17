<template>
  <header>
    <div class="container flex">
      <div class="left-section">
        <img src="../assets/streamflix-logo.png" alt="logo">
        <ul>
          <li><a href="">Home</a></li>
          <li><a href="">Serie TV</a></li>
          <li><a href="">Film</a></li>
          <li><a href="">Originali</a></li>
          <li><a href="">Aggiunti di recente</a></li>
          <li><a href="">La mia lista</a></li>
        </ul>
      </div>
      <div class="right-section flex">
        <form class="flex">
          <div class="input">
            <input type="text" class="form-control" placeholder="Cerca un film.." v-model.trim="searchItem" @keyup.enter="$emit('performSearch', searchItem)">
          </div>
          <button type="submit" class="btn btn-primary m-2" @click.prevent="$emit('performSearch', searchItem)">Cerca</button>
        </form>
        <img src="https://upload.wikimedia.org/wikipedia/commons/0/0b/Netflix-avatar.png" alt="user">
        <i class="fas fa-caret-down"></i>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data: function() {
      return {
          searchItem: ""
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

        .left-section {
          @include flex;

          img {
          height: 50px;
          }

          & ul {
            @include flex;
            list-style: none;
            margin: auto;
            padding-left: 10px;

            & li {
              margin-left: 12px;
              
              & a {
                text-decoration: none;
                color: $mainText;

                &:hover {
                  color: $mainRed;
                }
              }
            }
          }
        }

        .right-section img {
          margin-left: 6px;
          width: 30px;
          height: 30px;
        }

        .btn {
        background-color: $mainRed;
        border: 1px solid $mainRed;
        }

        i {
          margin-left: 6px;
          font-size: 16px;
          color: $mainText;
        }
      }


  }
</style>
