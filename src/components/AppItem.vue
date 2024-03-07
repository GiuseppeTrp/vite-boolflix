<script>
import { store } from "/store.js";

export default {
    name: 'AppItem',

    data() {
        return {
            store,
        }
    }
}
</script>

<template>
  <div class="d-flex justify-content-center bg-success ">
    <ul class=" container-fluid d-flex flex-column gap-2 unstyled-list  m-2 rounded" >
      <li  v-for="(movie, index) in store.movies" :key="index" class="card cards text-white border rounded bg-dark p-2 d-flex gap-2">
        <img :src="movie.backdrop_path" :alt="movie.original_title" class="border rounded  ">
        <div class="title">{{ movie.title }}</div>
        <div>{{ movie.overview }}</div>
      </li>
    </ul>

  </div>
 
</template>
  

<style lang="scss">











</style>