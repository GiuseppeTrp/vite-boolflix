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
    <nav class="navbar navbar-expand-lg  fixed-top border-bottom border-black border-5">
        <div class="container-fluid align-items-center container-fluid text-uppercase text-danger logo p-5">
            <form class="d-flex gap-1" role="search" @submit.prevent>
                <img class="rounded" src="../assets/img/logo-boolflix-mini.JPG" alt="">
                <input id="searchInput" v-model="store.selection" class="form-control me-2" type="search" placeholder="Search series/movies" aria-label="Search" @keyup.enter="$emit('search')">
                <button @click="$emit('search')" class="btn btn-outline-danger" type="button"><i class="fa fa-search"></i></button>
            </form>
        </div>
    </nav>
</template>


<style lang="scss">
@import '/src/general.scss';


.navbar{
    background-color: $bgColour;
    position: fixed;
}
h1{ 
   background-color: white;
   font-weight: bold;
}


.logo{
    background-image: url('../assets/img/BOOLFLIX.JPG');
    background-position: center;
    background-repeat: no-repeat;
    background-size:calc(100% / 6 * 2);
    cursor: pointer;
    
    
    

}
img{
    width: 30px;
    cursor: pointer;
    
    
}
</style>