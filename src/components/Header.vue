<template>
   <header>

      <p class="logo m-0">BOOLFLIX</p>

      <div class="search-bar">
         <input 
            v-model="stringToSearch"
            @keyup.enter="$emit('sendSearch', stringToSearch)"
            type="text" 
            class="form-control"
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
         font-size: 1.7rem;
         color: $logo-color;
      }
   }
</style>