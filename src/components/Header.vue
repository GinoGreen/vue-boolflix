<template>
   <header>

      <img src="../assets/img/boolflix-logo.png" class="logo" alt="boolflix logo">

      <div class="search-bar d-flex">
         <button 
            class="btn"
            @click="$emit('sendSearch', stringToSearch, contentType)"
         > Cerca
         </button>
         <input 
            v-model="stringToSearch"
            @keyup.enter="$emit('sendSearch', stringToSearch, contentType)"
            type="text" 
            class="form-control"
            placeholder="Cerca..."
         >
         <select 
            class="form-select"
            v-model="contentType"
         >
            <option value="all" selected>Tutti</option>
            <option value="movie">Film</option>
            <option value="tv">Serie TV</option>
         </select>
      </div>

   </header>
</template>

<script>
export default {
   name: 'Header',
   data() {
      return {
         stringToSearch: '',
         contentType: 'all'
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

         input {
            border-top-right-radius: 0;
            border-bottom-right-radius: 0;
         }
         select {
            max-width: 40px;
            border: none;

            // background-color: $logo-color;
            border-top-left-radius: 0;
            border-bottom-left-radius: 0;
            cursor: pointer;
         }
      }
   }
</style>