<script>
    import { store } from '/store.js';

    export default {
        data() {
            return {
                store, 
            }
        },
        name: 'AppHeader',
    }
</script>

<template>
    <!-- nav-->
    <nav class="navbar navbar-expand-lg  fixed-top border-bottom border-black border-5">
       
        <div class="container-fluid  justify-content-start   text-uppercase logo p-5">
            <!-- search -->
            <form class="d-flex gap-1 bg-black rounded p-1 " role="search" @submit.prevent>
                <!-- Logo -->
                <img class=" border border-black rounded " src="../assets/img/logo-boolflix-mini.JPG" alt="">
                <!-- Input di ricerca -->
                <input id="searchInput" v-model="store.selection" class="form-control me-2" type="search" placeholder="Search series/movies" aria-label="Search" @keyup.enter="$emit('search')">
                <!-- Pulsante di ricerca -->
                <button @click="$emit('search')" class="btn btn-outline-danger  " type="button"><i class="fa fa-search"></i></button>
            </form>
        </div>
    </nav>
</template>

<style lang="scss">
    @import '/src/general.scss';

 
    .navbar {
        background-color: $bgColour; 
        position: fixed; 
    }
    

    h1 { 
        background-color: white; 
        font-weight: bold; 
    }

    // Stili per il logo
    .logo {
        background-image: url('../assets/img/BOOLFLIX.JPG'); 
        background-position: center; 
        background-repeat:repeat-x; 
        background-size: calc(100% / 6) * 2; 
        cursor: pointer; 
    }

    // Stili per le immagini
    img {
        width: 30px; // Larghezza
        cursor: pointer; // Cursore
    }
</style>
