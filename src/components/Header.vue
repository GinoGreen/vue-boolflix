<template>
   <header>

      <img src="../assets/img/boolflix-logo.png" class="logo" alt="boolflix logo">

      <div class="search-bar d-flex">
         <button 
            class="btn"
            @click="$emit('sendSearch', stringToSearch)"
         > Cerca
         </button>
         <input 
            v-model="stringToSearch"
            @keyup.enter="$emit('sendSearch', stringToSearch)"
            type="text" 
            class="form-control"
            placeholder="Cerca..."
         >
      </div>

   </header>
</template>

<script>
export default {
   name: 'Header',
   data() {
      return {
         stringToSearch: ''
      }
   }
}
</script>

<style lang="scss">

@import '../assets/style/vars.scss';
@import '../assets/style/mixins.scss';

   header {
      height: 60px;
      padding: 10px;
      background-color: #000;

      @include center('align');
      justify-content: space-between;

      .logo {
         width: 170px;
         color: $logo-color;
         cursor: pointer;
      }

      .search-bar {
         width: 500px;

         button {
            width: 200px;
            margin: 0 20px;
            color: #fff;
            font-weight: bold;
            background-color: $logo-color;
         }
      }
   }
</style>