<template>
  <div id="app">

    <Header @sendSearch="collectSearch"/>

    <Main :query="stringToSearch"/>

  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'


export default {
  name: 'App',
  components: {
    Main,
    Header
  },
  data() {
    return {
      stringToSearch: ''
    }
  },
  methods: {
    collectSearch(string) {
      // console.log('string in app', string);
      this.stringToSearch = string;
    }
  }
}
</script>

<style lang="scss">

@import './assets/style/generals.scss';
// @import './assets/style/mixins.scss';

  
</style>
