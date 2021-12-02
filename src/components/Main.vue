<template>
   <main>

      <!-- FILMs -->
      <div class="movies">
         <div class="title">
            <h2 class="fw-bold">Film</h2>
            <p>Romantici, divertenti, drammatici, horror e tanto altro: solo i film sanno suscitare così tante emozioni. Un'ampia scelta di titoli per avventure infinite.</p>
         </div>
         <div class="myContainer">
            <Card 
               v-for="movie in contents.movie"
               :key="movie.id"
               :content="movie"
               :type="types.movie"
            />
         </div>
      </div>

      <!-- SERIE TVs -->
      <div class="tv-series">
         <div class="title">
            <h2 class="fw-bold">Serie TV</h2>
            <p>Oggi il piccolo schermo ha grandi cose da offrire: dalle sitcom ai drammi passando per i talk show, ecco i migliori programmi televisivi.</p>
         </div>
         <div class="myContainer">
            <Card 
               v-for="tv in contents.tv"
               :key="tv.id"
               :content="tv"
               :type="types.tv"
            />
         </div>
      </div>

   </main>
</template>

<script>
import Card from './Card.vue';
export default {
   components: {
      Card
   },
   name: 'Main',
   props: {
      contents: Object,
      types: Object
   },
   methods: {
      
   }
}
</script>

<style lang="scss">

@import '../assets/style/mixins.scss';

   main {
      height: calc(100vh - 60px);
      padding: 0 60px;
      color: #fff;

      background-color: #181818;
      overflow: auto;

      .title {
         width: 800px;

         h2 {
            margin: 30px 0;
            font-size: 3rem;
         }

         p {
            margin-bottom: 60px;
            font-size: 1.5rem;
         }
      }

      .myContainer {
         margin-bottom: 100px;
         padding: 30px 0;
         @include center('align');
         overflow-x: hidden;
      }
      
   }
</style>