<template>
   <main>
      <ul
         v-for="(film) in getSearch"
         :key="film.id"
      >
         <li>Titolo: {{ film.title }}</li>
         <li>Titolo originale: {{ film.original_title }}</li>
         <li>Lingua: {{ film.original_language }}</li>
         <li>Voto: {{ film.vote_average }}</li>
      </ul>
   </main>
</template>

<script>

import axios from 'axios';

export default {
   name: 'Main',
   props: {
      query: String
   },
   data() {
      return {
         films: [],
         isLoading: false
      }
   },
   methods: {
      async getApi() {
         this.isLoading = true;
         axios.get('https://api.themoviedb.org/3/search/movie', {
            params: {
               api_key: '8a381874b7779b2d846cc51434cc20f4',
               query: this.query
            }
         })
            .then(r => {
               console.log(r);
               this.films = r.data.results;
               console.log(this.films);
               this.isLoading = false
            })
            .catch(e => {
               console.log(e);
            });
      }
      
   },
   computed: {
      
      getSearch() {
         if (this.query === '') return this.films;
         console.log(this.query);
         this.getApi();
         return this.films;
      }
   },
   mounte() {
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
      }
   }
</style>