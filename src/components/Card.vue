<template>
   <div class="flip-card">
      <div class="flip-card-inner">
         <div class="flip-card-front">
            <!-- <img :src="getPoster()" alt="Poster" -->
         </div>
         <div class="flip-card-back">
            <h3 v-if="type === 'movie'">{{ content.title }}</h3>
            <h3 v-else>{{ content.name }}</h3>
            <h4 v-if="type === 'movie'">{{ content.original_title }}</h4>
            <p>
               Lingua: 
               <img 
                  class="original-language"
                  v-if="checkLanguage() !== ''"
                  :src="checkLanguage()"
                  :alt="content.original_language"
               >
               <span v-else>{{ content.original_language }}</span>
            </p> 
            <p>Voto: {{ content.vote_average }}</p>
         </div>
      </div>
   </div>
</template>

<script>
export default {
   name: 'Card',
   props: {
      content: Object,
      type: String
   },
   data() {
      return {
         imgURL: 'https://image.tmdb.org/t/p/w342/'
      }
   },
   methods: {
      checkLanguage() {
         const language = this.content.original_language;
         let imgPath = '';

         if (language.toLowerCase().includes('it')) return imgPath = require('../assets/img/it.png');
         if (language.toLowerCase().includes('en')) return imgPath = require('../assets/img/en.png');
         // altrimenti
         return imgPath;
      },
      getPoster() {
         // const composedImgURL = '';

         // composedImgUrl = this.imgURL + this.content
      }
   }
}
</script>

<style lang="scss">

@import '../assets/style/mixins.scss';

.flip-card {
   margin-right: 30px;
   background-color: transparent;
   width: 300px;
   height: 300px;
   perspective: 1000px;
         flex-shrink: 0;

   &:hover .flip-card-inner {
      transform: rotateY(180deg);
   }

   .flip-card-inner {
      position: relative;
      width: 100%;
      height: 100%;
      text-align: center;
      transition: transform 0.6s;
      transform-style: preserve-3d;
      box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);

      .flip-card-front, .flip-card-back {
         position: absolute;
         width: 100%;
         height: 100%;
         -webkit-backface-visibility: hidden;
         backface-visibility: hidden;
      }

      .flip-card-front {
         background-color: #bbb;
         color: black;
      }

      .flip-card-back {
         background-color: #2980b9;
         color: white;
         transform: rotateY(180deg);

         @include center();
         flex-direction: column;

         .original-language {
            width: 20px;
         }
      }
   }
}
</style>