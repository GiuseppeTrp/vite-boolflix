<script>

import AppItem from "./AppItem.vue";

import {store} from '/store.js';

export default {
    name: 'AppList',

    components:  {
        
        AppItem
    },

    data() {
        return  {
            store,
        }
    }
}
</script>

<template>
   

    <div class=" container-fluid p-5 border rounded d-flex flex-column justify-content center "> 


        <ul class="container-fluid p-5  bg-white  rounded">
            <div class="count text-uppercase container-fluid bg-dark text-white p-2 text-center">Found {{ store.movies.length }} movies</div>

            
            <AppItem  class="d-flex"
                v-for="movies in store.movies"
                :cards="movies"
            ></AppItem>
           
        </ul>
    </div>
</template>

<style lang="scss">





.count{
    font-weight: bolder;
}


</style>./CardsItem.vue/index.js