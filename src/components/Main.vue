<template>
   <main>

      <!-- FILMs -->
      <div class="movies">
         <h2>Film</h2>
         
      </div>

      <!-- SERIE TVs -->
      <div class="tv-series myContainer">
         <h2>Serie TV</h2>
         
      </div>

   </main>
</template>

<script>
export default {
   name: 'Main',
   props: {
      contents: Object
   },
   methods: {
      checkLanguage(content) {

         const language = content.original_language;
         let imgPath = '';

         if (language.toLowerCase().includes('it')) return imgPath = require('../assets/img/it.png');
         if (language.toLowerCase().includes('en')) return imgPath = require('../assets/img/en.png');
         // altrimenti
         return imgPath;
      }
   }
}
</script>

<style lang="scss">

@import '../assets/style/mixins.scss';

   main {
      height: calc(100vh - 60px);
      padding: 20px;
      color: #fff;

      background-color: #181818;
      overflow: auto;

      
      .movies, 
      .tv-series {
         display: flex;
         flex-wrap: wrap; 
      }
   }
</style>