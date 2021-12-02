<template>
   <main>

      <div class="movies">
         <ul
            v-for="(film) in films"
            :key="film.id"
         >
            <li>Titolo: {{ film.title }}</li>
            <li>Titolo originale: {{ film.original_title }}</li>
            <li>Lingua: 
               <img 
                  class="original-language"
                  v-if="checkLanguage(film) !== ''"
                  :src="checkLanguage(film)" 
                  :alt="film.original_language"
               >
               <span v-else>
                  {{ film.original_language }}
               </span>
            </li>
            <li>Voto: {{ film.vote_average }}</li>
         </ul>
      </div>

      <div class="tv-series">

      </div>

   </main>
</template>

<script>
export default {
   name: 'Main',
   props: {
      films: Array,
      tvSeries: Array
   },
   methods: {
      checkLanguage(movie) {

         const language = movie.original_language;
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
      color: #fff;

      display: flex;
      flex-wrap: wrap;

      background-color: #181818;
      overflow: auto;

      ul {
         padding: 0;
         margin: 20px;
         background-color: grey; //da rimuovere

         .original-language {
            width: 20px;
         }
      }
   }
</style>