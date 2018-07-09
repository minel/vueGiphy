<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld msg="Wilkommen to Your Vue.js App"/>
    <search v-on:SearchRequested="handleSearch"></search>
    <img v-if="isLoading" id="loading" src="https://media.giphy.com/media/3o7bu3XilJ5BOiSGic/giphy.gif" />
    <preview v-bind:gifs="gifs"></preview>
  </div>
</template>

<script>
//You can use :gifs instead of v-bind:gifs
import HelloWorld from './components/HelloWorld.vue';
import Search from './components/Search.vue';
import Preview from './components/Preview.vue';

export default {
  name: 'app',
  components: {
    HelloWorld,
    Search,
    Preview
  },
  data() {
    return {
      isLoading: true,
      gifs: []
    }
  },
  created() {
    const url = 'https://api.giphy.com/v1/gifs/trending?api_key=oBU3tUzh4KH5xzn43FT607TMlpF1InjR&limit=25&rating=G';
    console.log('created: Request sending ->', url);
    this.doQuery(url);
  },
  methods: {
    doQuery(url) {
      console.log('start doQuery');
      fetch(url)
        .then((res) => {
          return res.json();
        })
        .then((res) => {
          console.log('promise tamam');
          this.gifs = res.data;
          this.isLoading = false;
        });
    },
    handleSearch(query) {
      this.gifs = [];
      this.isLoading = true;
      console.log('handleSearch:', query ? query : '<empty>');
      const url = `https://api.giphy.com/v1/gifs/search?api_key=oBU3tUzh4KH5xzn43FT607TMlpF1InjR&q=${query}&limit=25&rating=G`;
      console.log('handleSearch: Request sending ->', url);
      this.doQuery(url);
      console.log('a line after request');
      }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#loading {
  padding-top: 20px;
}
</style>
