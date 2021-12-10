<template>
  <div id="app">

    <Header 
      @sendSearch="collectSearch"
      @typeChanged="collectType"
    />

    <Main 
      :contents="contents"
      :types="types"
      :firstCall="firstCallAxios"
      :stringSearched="query"
      :isLoading="isLoading"
      :typeSelected="typeSelected"
    />

  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios';


export default {
  name: 'App',
  components: {
    Main,
    Header
  },
  data() {
    return {
      firstCallAxios: true,
      query: '',
      types: {
        movie: 'movie',
        tv: 'tv',
      },
      typeSelected: 'all',
      contents: {
        movie: [],
        tv: []
      },
      apiURL: 'https://api.themoviedb.org/3/search/',
      isLoading: false
    }
  },
  methods: {
    collectSearch(stringToSearch) {

      if (stringToSearch !== '') {

        // prima chiamata finita
        this.firstCallAxios = false

        this.query = stringToSearch;
        //chiamata Api
        this.getApi(this.types.movie);
        this.getApi(this.types.tv);
      }
    },
    collectType(type) {
      this.typeSelected = type;
    },
    getApi(typeOfContent) {

      this.isLoading = true;

      let composedApiURL = '';
      //controllo prima chiamata
      if (this.firstCallAxios) {
        composedApiURL = `https://api.themoviedb.org/3/${typeOfContent}/popular`;
      }
      else {
        composedApiURL = this.apiURL + typeOfContent;
      }

      axios.get(composedApiURL, {
        params: {
            api_key: '8a381874b7779b2d846cc51434cc20f4',
            query: this.query
        }
      })
        .then(r => {

            console.log('typeOfContent', typeOfContent);

            this.contents[typeOfContent] = r.data.results;

            console.log('film e serie', this.contents);
            // console.log('film', this.contents.movie);
            // console.log('tv', this.contents.tv);

            //caricamento completato
            this.isLoading = false
        })
        .catch(e => {
          console.log(e);
        });
    }
  },
  mounted() {
    this.getApi(this.types.movie);
    this.getApi(this.types.tv);
  }
}
</script>

<style lang="scss">

@import './assets/style/generals.scss';
// @import './assets/style/mixins.scss';

  
</style>
