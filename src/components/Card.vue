<template>
   <div class="flip-card">
      <div class="flip-card-inner">
         <div class="flip-card-front">
            <div v-if="content.poster_path === null" class="poster-placeholder">
               <h3 class="mt-5 text-white">Poster non disponibile</h3>
               <img src="../assets/img/placeholder.jpg" alt="placeholder not found">
            </div>
            <img v-else :src="getPoster()" alt="Poster">
         </div>
         <div class="flip-card-back">
            <div class="info-topside">
               <h5 v-if="type === 'movie'">{{ content.title }}</h5>
               <h5 v-else>{{ content.name }}</h5>
               <h5 v-if="type === 'movie'">{{ content.original_title }}</h5>
               <h5 v-else>{{ content.original_name }}</h5>
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
               <p>Voto: 
                  <i 
                     v-for="(star, index) in MAX_STARS"
                     :key="index"
                     class="fa-star"
                     :class="[index < getStars(content.vote_average) ? 'fas' : 'far']"
                  ></i>
               </p>
            </div>
            <div class="caption">
               <p>{{ content.overview }}</p>
            </div>
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
         imgURL: 'https://image.tmdb.org/t/p/w342/',
         composedImgURL: '',
         MAX_STARS: 5
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
         return this.composedImgURL = this.imgURL + this.content.poster_path
      },
      getStars(n) {
         return Math.round(n/2);
      }
   }
}
</script>

<style lang="scss">

@import '../assets/style/mixins.scss';
@import '~@fortawesome/fontawesome-free/css/all.min.css';

.flip-card {
   margin-right: 40px;
   background-color: transparent;
   width: 200px !important;
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

      h5 {
         font-size: 1.1em;
      }
      p {
         margin: 0;
      }

      .flip-card-front, .flip-card-back {
         position: absolute;
         width: 100%;
         height: 100%;
         -webkit-backface-visibility: hidden;
         backface-visibility: hidden;
      }

      .flip-card-front {
         background-color: #4D4D4D;
         color: black;

         overflow: hidden;
         
         img {
            height: 100%;
         }

         .poster-placeholder img {
            width: 100%;
         }
      }

      .flip-card-back {
         padding: 10px;
         background-color: #2e3035;
         color: white;
         transform: rotateY(180deg);

         i.fa-star {
            color: #d1a640;
         }

         .original-language {
            width: 20px;
         }

         .info-topside {
            height: 50%;
            overflow: auto;
         }

         .caption {
            height: 50%;
            overflow: auto;
            text-align: start;
         }
      }
   }
}
</style>