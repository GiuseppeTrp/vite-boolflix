<script>
    import { store } from '/store.js';
    import AppItem from './AppItem.vue';

    export default {
        data() {
            return {
                store, 
            }
        },
     
        name: 'AppList',
      
        components: {
            AppItem,
        },
    }
</script>

<template>
    <!-- Contenitore principale per i film -->
    <div class=" background container-fluid  p-5 text-white mt-5 border-bottom border-black border-5">
        <!-- Titolo dei film -->
        <h3 class="text-white">Movies</h3>

        <!-- Contenitore per le card dei film -->
        <div class="  cards d-flex flex-wrap  p-2 gap-1 justify-content-center">
            <!-- Iterazione attraverso i film nello store -->
            <AppItem v-for="currentMovie in store.movies" :key="currentMovie.id"
                :imageCover="currentMovie.poster_path"
                :titleMovie="currentMovie.title" :originalTitle="currentMovie.original_name"
                :language="currentMovie.original_language"
                :vote="currentMovie.vote_average"
                :overview="currentMovie.overview">
            </AppItem>
        </div>
    </div>

    <!-- Contenitore principale per le serie -->
    <div class="container-fluid background  p-5  text-white " >
        <!-- Titolo delle serie -->
        <h3>Series</h3>
        <!-- Contenitore per le card delle serie -->
        <div class="cards d-flex flex-wrap p-2 gap-1 justify-content-center">
            <!-- Iterazione attraverso le serie nello store -->
            <AppItem v-for="currentSerie in store.series" :key="currentSerie.id"
                :imageCover="currentSerie.poster_path"
                :titleSerie="currentSerie.name" :originalTitle="currentSerie.original_name"
                :language="currentSerie.original_language"
                :vote="currentSerie.vote_average"
                :overview="currentSerie.overview">
            </AppItem>
        </div>
    </div>
</template>

<style lang="scss">
    @import '/src/general.scss';

   
    .background {
        background-color: $bgColour; 
        position: relative; 
        top: 100px; 
    }
</style>
