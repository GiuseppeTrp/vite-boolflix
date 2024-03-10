<script>
import { store } from '/store.js';

export default {
    
    data() {
        return {
            store,
        }
    },

    props: {
        imageCover: String,      
        titleMovie: String,      
        titleSerie: String,     
        originalTitle: String,  
        language: String,      
        vote: Number,       
        overview: String,    
    },

    name: 'AppItem',
    methods: {
    transformVote(vote) {
        // Calcola il numero di stelle piene intere dividendo il voto per 2 e arrotondando per difetto(per averne massimo 5)
        const numFullStars = Math.floor(vote / 2); 

        // Verifica se c'è una mezza stella
        let hasHalfStar = false;
        if (vote % 2 !== 0) {
            hasHalfStar = true;
        }

        // Calcola il numero di stelle vuote
        let numEmptyStars = 5 - numFullStars;
        if (hasHalfStar) {
            numEmptyStars -= 1; // Sottrae una stella vuota se c'è una mezza stella
        }

        // Restituisce un oggetto contenente il numero di stelle piene, se c'è una mezza stella e il numero di stelle vuote rimanenti
        return { numFullStars, hasHalfStar, numEmptyStars };
    }
 }

}

</script>

<template>
    <!-- Componente della card -->
    <div class="card bg-dark ">
        <!-- Immagine della card -->
        <div class="card-img bg-dark">
            <!-- Controllo se è presente un'immagine di copertina, altrimenti mostro un'immagine di fallback -->
            <img v-if="imageCover !== null" :src="'https://image.tmdb.org/t/p/w342' + imageCover" alt="">
            <img v-else src="../assets/img/no-cover.JPG" alt="image not found">
        </div>
        <!-- Corpo della card -->
        <div class="card-body ">
            <!-- Titolo del film -->
            <h5 class="card-title text-white">{{ titleMovie }}</h5>
            <!-- Titolo originale del film -->
            <h6 class="card-subtitle mb-2 text-white ">{{ originalTitle }}</h6>
                <!-- Voto del film -->
                
<h6 class="card-subtitle mb-2 text-white">
    <!-- Inizia la sezione delle stelle piene -->
    <!-- Utilizza una direttiva v-for per iterare attraverso il numero di stelle piene -->
    <span v-for="index in transformVote(vote).numFullStars" :key="'star-' + index" class="fa fa-star"></span>
    <!-- Fine della sezione delle stelle piene -->

    <!-- Sezione della mezza stella, se necessario -->
    <!-- Utilizza una direttiva v-if per condizionare la visualizzazione della mezza stella -->
                <span v-if="transformVote(vote).hasHalfStar" class="fa fa-star-half-o"></span>
                <!-- Fine della sezione della mezza stella -->

               
                <!-- itero attraverso il numero di stelle vuote rimanenti -->
                <span v-for="index in transformVote(vote).numEmptyStars"   class="fa fa-star-o"></span>
               
            </h6>

            <!-- Lingua del film -->
            <div class="flag">
                <img v-if="language == 'it'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/it.webp" alt="Italy Flag">
                <img v-else-if="language == 'en'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/gb.webp" alt="UK Flag">
                <img v-else-if="language == 'en-us'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/us.webp" alt="USA Flag">
                <img v-else-if="language == 'nl'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/us.webp" alt="Germany Flag">
                <img v-else-if="language == 'fr'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/fr.webp" alt="France Flag">
                <img v-else-if="language == 'es'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/es.webp" alt="Spain Flag">
                <img v-else-if="language == 'ko'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/kr.webp" alt="Korea Flag">
                <img v-else-if="language == 'ja'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/jp.webp" alt="Japan Flag">
                <img v-else-if="language == 'zh-cn'" class="img-fluid" src="https://flagpedia.net/data/flags/w550/cn.webp" alt="China Flag">
                <img class="text-white" v-else src="" alt="no lang flag">
            </div>
            <!-- Panoramica del film -->
            <p class="card-text font-weight-bold text-warning">
                overview:
                <small class="font-italic text-white" v-if="overview">{{ overview }}</small>
                <small class="font-italic text-white" v-else>Not Found.</small>
            </p>        
        </div>
    </div>
</template>

<style lang="scss" scoped>
/* Stili CSS per il componente */

/* Stili per la card */
.card {
    width: calc(100% / 5);
}

/* Stili per l'immagine della card */
.card .card-img img {
    width: 100%;
}

/* Stili per il corpo della card */
.card .card-body {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0;
    transition: opacity .3s;
}

/* Stili per il testo della card */
.card-text{
    line-height: 1;
    max-height: 200px ;
    overflow-y:scroll;
}

/* Stili per l'hover sul componente */
.card:hover .card-body {
    opacity: 1;
}

.card:hover .card-img {
    opacity: 0.5;
}

/* Stili per la scrollbar */
.card-text::-webkit-scrollbar {
    width: 10px; /* Larghezza della scrollbar */
    background-color: rgba(128, 128, 128, 0); /* Sfondo della scrollbar */
}

</style>

