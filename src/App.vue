<template>
  <div id="app">

    <Header @sendSearch="collectSearch"/>

    <Main :films="films" :tvSeries="tvSeries"/>

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
      query: '',
      // typeOfContent: 'movie'
      films: [],
      tvSeries: [],
      apiURL: 'https://api.themoviedb.org/3/search/',
      isLoading: false
    }
  },
  methods: {
    collectSearch(string) {

      this.query = string;
      //chiamata Api
      this.getApi('movie', this.films);
      this.getApi('tv', this.tvSeries);
    },
    getApi(typeOfContent, contents) {

      this.isLoading = true;
      
      axios.get(this.apiURL + typeOfContent, {
        params: {
            api_key: '8a381874b7779b2d846cc51434cc20f4',
            query: this.query
        }
      })
        .then(r => {
          //  console.log(this.query);
            contents = r.data.results;
            console.log(this.films);
            //caricamento completato
            this.isLoading = false
        })
        .catch(e => {
          console.log(e);
        });
    }
  }
}
</script>

<style lang="scss">

@import './assets/style/generals.scss';
// @import './assets/style/mixins.scss';

  
</style>
