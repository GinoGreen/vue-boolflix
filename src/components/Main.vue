<template>
   <main>
      <ul
         v-for="(film) in films"
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
export default {
   name: 'Main',
   props: {
      films: Array
   },
   data() {
      return {
      }
   },
   methods: {
      
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