<script>
import axios from 'axios';

import { store } from '/store.js';

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
// Metodo che viene chiamato quando il componente viene creato
created() {
        this.movieSeries(); // Invoca la funzione per ottenere i film e le serie popolari
    },
    // Metodi del componente
    methods: { 
        // Funzione per ottenere i film e le serie popolari
        movieSeries() {
            // Richiesta per ottenere i film popolari
            axios
                .get(`https://api.themoviedb.org/3/movie/popular?api_key=ef84164b24031cff967786824de7194f&language=it`)
                .then(res => {
                    this.store.movies = res.data.results; // Aggiorna i film nello store con i risultati ottenuti dalla richiesta
                });

            // Richiesta per ottenere le serie TV popolari
            axios
                .get(`https://api.themoviedb.org/3/tv/popular?api_key=ef84164b24031cff967786824de7194f&language=it`)
                .then(res => {
                    this.store.series = res.data.results; // Aggiorna le serie TV nello store con i risultati ottenuti dalla richiesta
                });
        },
        // Funzione per cercare film e serie TV in base alla query inserita dall'utente
        selected() {
            // Richiesta per cercare i film in base alla query inserita dall'utente
            axios
                .get(`https://api.themoviedb.org/3/search/movie?api_key=ef84164b24031cff967786824de7194f&language=it_IT&query=${this.store.selection}`)
                .then(res => {
                    this.store.movies = res.data.results; // Aggiorna i film nello store con i risultati ottenuti dalla ricerca
                });

            // Richiesta per cercare le serie TV in base alla query inserita dall'utente
            axios
                .get(`https://api.themoviedb.org/3/search/tv?api_key=ef84164b24031cff967786824de7194f&language=it_IT&query=${this.store.selection}`)
                .then(res => {
                    this.store.series = res.data.results; // Aggiorna le serie TV nello store con i risultati ottenuti dalla ricerca
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

<style></style>
