<template>
  <div class="movie-detail">
    <h2>{{movie.Title}}</h2>
    <p>{{movie.Year}}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img"/>
    <p>{{movie.Plot}}</p>
  </div>  
</template>

<script>
import{ref, onBeforeMount} from 'vue';
import { useRoute } from 'vue-router';

export default {
  setup(){
   const movie =ref({});
   const route = useRoute()
   //call Lifecycle hook
   onBeforeMount(()=>{
    //router link id
    fetch(`http://www.omdbapi.com/?apikey=${process.env.VUE_APP_API_KEY}&i=${route.params.id}&plot=full`)
    .then((res=> res.json()))
    .then((data=> movie.value = data)) //ref movie 
  })
  return {
    movie
   }
  }}
</script>

<style lang="scss">
  .movie-detail {
    padding: 16px;
    h2 {
      color: #FFF;
      font-size: 28px;
      font-weight: 600;
      margin-bottom: 16px;
    }
    .featured-img {
      display: block;
      max-width: 200px;
      margin-bottom: 16px;
    }
    p {
      color: #FFF;
      font-size: 18px;
      line-height: 1.4;
    }
  }
  </style>