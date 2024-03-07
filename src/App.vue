<script>
import { store } from "/store.js";
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppList from './components/AppList.vue';

export default {
  components: {
    AppHeader,
    AppList,
  },
  created() {
  },
  mounted() {
    this.searchMovies();
  },
  methods: {
    searchMovies() {
      axios
        .get('https://api.themoviedb.org/3/movie/popular?api_key=ef84164b24031cff967786824de7194f&language=it&q=ciao')
        .then(res => {
          console.log(res.data.results);
          store.movies = res.data.results;
        })
        .catch(error => {
          console.error('Hai sbagliato qualcosa:', error);
        });
    }
  }
}
</script>

<template>
<AppHeader></AppHeader>
<AppList></AppList>

</template>

<style scoped>

</style>
