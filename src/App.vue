<template>
  <div id="app">

    <Header @sendSearch="collectSearch"/>

    <Main :contents="contents"/>

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
      contents: {},
      apiURL: 'https://api.themoviedb.org/3/search/',
      isLoading: false
    }
  },
  methods: {
    collectSearch(string) {

      this.query = string;
      //chiamata Api
      this.getApi('movie');
      this.getApi('tv');
    },
    getApi(typeOfContent) {

      this.isLoading = true;
      
      axios.get(this.apiURL + typeOfContent, {
        params: {
            api_key: '8a381874b7779b2d846cc51434cc20f4',
            query: this.query
        }
      })
        .then(r => {

            console.log('typeOfContent', typeOfContent);

            this.contents[typeOfContent] = r.data.results;

            console.log('film e serie', this.contents);
            console.log('film', this.contents.movie);
            console.log('tv', this.contents.tv);

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
