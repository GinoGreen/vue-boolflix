<template>
  <div id="app">

    <Header @sendSearch="collectSearch(), getApi()"/>

    <Main :films="films"/>

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
      films: [],
      apiURL: 'https://api.themoviedb.org/3/search/movie',
      isLoading: false
    }
  },
  methods: {
    collectSearch(string) {
      // console.log('string in app', string);
      this.query = string;
    },
    getApi() {
         this.isLoading = true;
         axios.get(this.apiURL, {
            params: {
               api_key: '8a381874b7779b2d846cc51434cc20f4',
               query: this.query
            }
         })
            .then(r => {
               console.log(this.query);
               this.films = r.data.results;
               console.log(this.films);
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
