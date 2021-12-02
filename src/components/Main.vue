<template>
   <main>

      <!-- FILMs -->
      <div class="movies">
         <ul
            v-for="(film) in contents.movie"
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

      <!-- SERIE TVs -->
      <div class="tv-series">
         <ul
            v-for="(serie) in contents.tv"
            :key="serie.id"
         >
            <li>Titolo: {{ serie.title }}</li>
            <li>Titolo originale: {{ serie.original_title }}</li>
            <li>Lingua: 
               <img 
                  class="original-language"
                  v-if="checkLanguage(serie) !== ''"
                  :src="checkLanguage(serie)" 
                  :alt="serie.original_language"
               >
               <span v-else>
                  {{ serie.original_language }}
               </span>
            </li>
            <li>Voto: {{ serie.vote_average }}</li>
         </ul>
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
      color: #fff;

      background-color: #181818;
      overflow: auto;

      .movies {
                     display: flex;
            flex-wrap: wrap; 
         ul {
            padding: 0;
            margin: 20px;
            background-color: grey; //da rimuovere

         }
      }
      .tv-series {
                     display: flex;
            flex-wrap: wrap; 
         ul {
            background-color: teal; //da rimuovere
         }
      }

      .original-language {
         width: 20px;
      }
   }
</style>