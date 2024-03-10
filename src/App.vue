<script>
// Importo Axios per fare richieste HTTP
import axios from 'axios';

// Importo il file store.js che contiene lo stato dell'applicazione
import { store } from '/store.js';

// Importo i componenti Vue che sono stati definiti altrove nel codice
import AppList from './components/AppList.vue';
import AppHeader from './components/AppHeader.vue';

export default {
  components: {
    
    AppList,
    AppHeader,
  },
  data() {
    return {
      store,
    };
  },
  created() {
    this.movieSeries();
  },
  methods: { 
    movieSeries() {
      axios
        .get(`https://api.themoviedb.org/3/movie/popular?api_key=ef84164b24031cff967786824de7194f&language=it`)
        .then(res => {
          this.store.movies = res.data.results;
        });

      axios
        .get(`https://api.themoviedb.org/3/tv/popular?api_key=ef84164b24031cff967786824de7194f&language=it`)
        .then(res => {
          this.store.series = res.data.results;
        });
    },
    selected() {
      axios
        .get(`https://api.themoviedb.org/3/search/movie?api_key=ef84164b24031cff967786824de7194f&language=it_IT&query=${this.store.selection}`)
        .then(res => {
          this.store.movies = res.data.results;
        });

      axios
        .get(`https://api.themoviedb.org/3/search/tv?api_key=ef84164b24031cff967786824de7194f&language=it_IT&query=${this.store.selection}`)
        .then(res => {
          this.store.series = res.data.results;
        });
    },
  }
}
</script>

<template>
  <!-- Utilizzo il componente AppHeader per mostrare l'intestazione dell'applicazione -->
  <AppHeader @search="selected()"></AppHeader>
  
  <!-- Utilizzo il componente AppList per mostrare una lista di film o serie TV -->
  <AppList></AppList>
</template>

<!-- Stili CSS per questo componente -->
<style></style>
