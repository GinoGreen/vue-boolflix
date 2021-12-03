<template>
   <main>

      <!-- FILMs -->
      <div v-if="contents.movie.length > 0" class="movies">
         <div class="title">
            <h2 class="fw-bold">Film</h2>
            <p class="m-0">Romantici, divertenti, drammatici, horror e tanto altro: solo i film sanno suscitare così tante emozioni. Un'ampia scelta di titoli per avventure infinite.</p>
         </div>
         <div class="myContainer">
            <Card 
               v-for="movie in contents.movie"
               :key="movie.id"
               :content="movie"
               :type="types.movie"
            />
            <button class="btn-right">
               <span class="arrow">&#8250;</span>
            </button>
         </div>
      </div>

      <!-- SERIE TVs -->
      <div v-if="contents.tv.length > 0" class="tv-series">
         <div class="title">
            <h2 class="fw-bold">Serie TV</h2>
            <p class="m-0">Oggi il piccolo schermo ha grandi cose da offrire: dalle sitcom ai drammi passando per i talk show, ecco i migliori programmi televisivi.</p>
         </div>
         <div class="myContainer">
            <Card 
               v-for="tv in contents.tv"
               :key="tv.id"
               :content="tv"
               :type="types.tv"
            />
            <button class="btn-right">
               <span class="arrow">&#8250;</span>
            </button>
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

@import '../assets/style/vars.scss';
@import '../assets/style/mixins.scss';
// @import '';

   main {
      height: calc(100vh - 60px);
      padding: 60px;
      color: #fff;

      background-color: #181818;
      overflow: auto;

      .title {
         width: 45%;

         h2 {
            font-size: 3rem;
         }
      }

      .myContainer {
         max-width: 100%;
         padding: 70px 0;
         @include center('align');
         overflow-x: hidden;
         position: relative;
      }

      .btn-right {
         height: 100%;
         width: 100px;
         position: absolute;
         right: 0px;
         
         border: none;
         background-color: transparent;
         background-image: linear-gradient(to left,#181818 10%,rgba(24,24,24,0));


         &:hover .arrow {
            font-size: 5rem;

         }
         .arrow {
            position: absolute;
            right: 0;
            top: 50%;
            transform: translate(-50%, -50%);

            color: $logo-color;
            font-size: 3rem;


            transition: all 0.4s;
         }
      }
      
   }
</style>