<template>
   <main>

      <Loading 
         v-if="isLoading" 
         titleLoader="Caricamento contenuti..." 
      />

      <!-- nessun risultato -->
      <div 
         v-else-if="
            contents.movie.length === 0 &&
            contents.tv.length === 0 || 
            stringSearched === '' && 
            !firstCall
         ">
         <h1>Nessun risultato trovato per "{{ stringSearched }}"</h1>
      </div>

      <section v-else class="contents">
         <!-- FILMs -->
         <div v-if="contents.movie.length > 0" class="movies">

            <p v-if="!firstCall" class="caption-searched text-end">Risultati per <strong>"{{ stringSearched }}"</strong></p>

            <div class="title">
               <div v-if="firstCall"> <!--prima chiamata axios -->
                  <h2 class="fw-bold">Film popolari</h2>
                  <p class="m-0">Romantici, divertenti, drammatici, horror e tanto altro: solo i film sanno suscitare così tante emozioni. Un'ampia scelta di titoli per avventure infinite.</p>
               </div>
               <div v-else> <!--dopo la prima ricerca -->
                  <h2 class="fw-bold">Film</h2>
               </div>
            </div>

            <div class="myContainer">
               <button 
                  @click="showPrev('movie')"
                  class="btn-left"
                  v-if="contents.movie.length > 5"
               >
                  <span class="arrow left">&#8249;</span>
               </button>
               <VueSlickCarousel 
                  v-bind="settings"
                  ref="carouselMovie"
               >
                  <Card 
                     v-for="movie in contents.movie"
                     :key="movie.id"
                     :content="movie"
                     :type="types.movie"
                  />
               </VueSlickCarousel>
               <button 
                  @click="showNext('movie')" 
                  class="btn-right"
                  v-if="contents.movie.length > 5"
               >
                  <span class="arrow right">&#8250;</span>
               </button>
            </div>

         </div>

         <!-- SERIE TVs -->
         <div v-if="contents.tv.length > 0" class="tv-series">

            <div class="title">
               <div v-if="firstCall"> <!--prima chiamata axios -->
                  <h2 class="fw-bold">Serie TV Popolari</h2>
                  <p class="m-0">Oggi il piccolo schermo ha grandi cose da offrire: dalle sitcom ai drammi passando per i talk show, ecco i migliori programmi televisivi.</p>
               </div>
               <div v-else> <!--dopo la prima ricerca -->
                  <h2 class="fw-bold">Serie TV</h2>
               </div>
            </div>

            <div class="myContainer">
               <button 
                  @click="showPrev('tv')" 
                  class="btn-left"
                  v-if="contents.tv.length > 5"
               >
                  <span class="arrow left">&#8249;</span>
               </button>
               <VueSlickCarousel 
                  v-bind="settings"
                  ref="carouselTv"
               >
                  <Card 
                     v-for="tv in contents.tv"
                     :key="tv.id"
                     :content="tv"
                     :type="types.tv"
                  />
               </VueSlickCarousel>
               <button 
                  @click="showNext('tv')" 
                  class="btn-right"
                  v-if="contents.tv.length > 5"
               >
                  <span class="arrow right">&#8250;</span>
               </button>

            </div>

         </div>
      </section>

   </main>
</template>

<script>

import Card from './Card.vue';
import VueSlickCarousel from 'vue-slick-carousel'
import 'vue-slick-carousel/dist/vue-slick-carousel.css'
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css'
import Loading from './Loading.vue';

export default {
   components: {
      Card,
      VueSlickCarousel,
      Loading
   },
   name: 'Main',
   props: {
      contents: Object,
      types: Object,
      firstCall: Boolean,
      stringSearched: String,
      isLoading: Boolean
   },
   data() {
      return {
         settings: {
            "dots": false,
            "focusOnSelect": true,
            "infinite": false,
            "speed": 500,
            "slidesToShow": 1,
            "slidesToScroll": 3,
            "touchThreshold": 0,
            "variableWidth": true,
            "variableHeight": true
         }
      }
   },
   methods: {
      showNext(type) {
         if (type === 'movie') this.$refs.carouselMovie.next();
         else this.$refs.carouselTv.next();
      },
      showPrev(type) {
         if (type === 'movie') this.$refs.carouselMovie.prev();
         else this.$refs.carouselTv.prev();
      },
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

      // @include center();

      background-color: #181818;
      overflow: auto;

      .caption-searched {
         font-size: 1.4rem;
      }
      .title {
         width: 45%;

         h2 {
            font-size: 3rem;
         }
      }
      

      .myContainer {
         max-width: 100%;
         height: 400px;
         @include center('align');
         overflow-x: hidden;
         position: relative;

         .slick-slider.slick-initialized,
         .slick-list {
            height: 100% !important;
            @include center('align');
         }
      }

      .btn-right,
      .btn-left {
         height: 100%;
         width: 100px;
         position: absolute;

         border: none;
         background-color: transparent;

         z-index: 200;

         &:hover .arrow {
            font-size: 5rem;
         }
      }

      .arrow {
         position: absolute;
         top: 50%;

         color: $logo-color;
         font-size: 3rem;

         transition: all 0.4s;
         
         &.left {
            left: 0;
            transform: translate(50%, -50%);
         }
         &.right {
            right: 0;
            transform: translate(-50%, -50%);
         }
      }

      .btn-right {
         right: 0px;
         background-image: linear-gradient(to left,#181818 10%,rgba(24,24,24,0));
      }
      .btn-left {
         left: 0px;
         background-image: linear-gradient(to right,#181818 10%,rgba(24,24,24,0));
      }
      
   }
</style>