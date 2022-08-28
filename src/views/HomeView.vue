<template>
  <div class="home">
    <div class="feature-card">
      <!--  to movie id -->
      <router-link to="/movie/tt0409591">
        <img src="https://img.freepik.com/premium-photo/movie-clapper-red-background-with-copy-space_23-2148416747.jpg?w=1480" alt="Naruto Poster" class="featured-img" />
        <div class="detail">
          <!-- <h3>Naruto</h3> -->
          <!-- <p>Naruto Uzumaki, a mischievous adolescent ninja, struggles as he searches for recognition and dreams of becoming the Hokage, the village's leader and strongest ninja.</p> -->
      
    </div>
  </router-link>
  <!-- fetch search movies and call the function -->
  <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search" />
      <input type="submit" value="Search"  />
    </form>

      <div class="movie-list">
        <!-- loop moive array -->
        <div class="movie" v-for="(movie,index) in movies" :key="index">
          <router-link to="'/movie/' + movie.imdbID" class="movie-link">
            <div class="product-image">
              <img :src='movie.Poster' alt="Movie Poster"/>
              <div class="type">{{movie.Type}}</div>
            </div>
            <div class="detail">
              <h3>{{movie.Title}}</h3>
              <div class="y">{{movie.Year}}</div>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src and use for router
// import HelloWorld from '@/components/HelloWorld.vue'
//http://www.omdbapi.com/?s=Batman&page=2

import{ref} from "vue";
//import apikey
//import env from '.@/env.js'



export default {
  setup(){
    const search = ref('');
    const movies = ref([])

    //fetch the movie api
    const SearchMovies =()=>{
      const apikey = '210e1944';
      if(search.value !==""){
        fetch(`http://www.omdbapi.com/?i=tt3896198&apikey=${apikey}&s=${search.value}`)
        .then((response)=>response.json())
        .then((data)=>{
          //array movie 
          movies.value= data.Search
          //reset the search bar
          search.value = ''
          console.log(movies.value)
        }
        
      )}
    
    }

    return {
      search,
      movies,
      SearchMovies

    }

  }

  
}
</script>


<style lang="scss">
 .home {
  .feature-card {
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;

      /* position: relative;
      z-index: 0; */
    }

    .detail {
      /* position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: 1; */
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;

      h3 {
        color:#FFF;
        margin-bottom: 16px;
      }

      p {
        color: #FFF;
      }
    }
  }
 }
  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        color: #FFF;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #42B883;
        padding: 16px;
        border-radius: 8px;
        color: #FFF;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: #3B8070;
        }
      }
    }
  }

  .movie-list{
    margin: 30px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    gap:5%;
  }
  



</style>
