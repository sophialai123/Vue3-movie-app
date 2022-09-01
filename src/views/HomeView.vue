<template>
  <div class="home">
    <div class="feature-card">
      <!--  to movie id -->
      <router-link to="/movie/tt2361509">
        <img
          src="https://img.freepik.com/premium-photo/movie-clapper-red-background-with-copy-space_23-2148416747.jpg?w=1480"
          alt="Naruto Poster"
          class="featured-img"
        />
        <div class="detail"></div>
      </router-link>
      <!-- fetch search movies and call the function -->
      <form @submit.prevent="SearchMovies()" class="search-box">
        <input
          type="text"
          placeholder="What are you looking for?"
          v-model="search"
        />
        <input type="submit" value="Search" />
      </form>
      <div class="movies-list">
        <!-- loop moive array -->
        <div class="movie" v-for="movie in movies" :key="movie.imdbID">
          <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
            <div class="detail">
              <h3>{{ movie.Title }}</h3>
              <div class="year">{{ movie.Year }}</div>
            </div>
            <div class="product-image">
              <img :src="movie.Poster" alt="Movie Poster" />
              <div class="type">{{ movie.Type }}</div>
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

import { ref } from "vue";
//import apikey
//import env from '.@/env.js'

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    //fetch the movie api
    const SearchMovies = () => {
      if (search.value !== "") {
        fetch(
          `http://www.omdbapi.com/?i=tt3896198&apikey=${process.env.VUE_APP_API_KEY}&s=${search.value}`
        )
          .then((response) => response.json())
          .then((data) => {
            //array movie
            movies.value = data.Search;
            //reset the search bar
            search.value = "";
            //console.log(movies.value);

            console.log(data);
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
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
        color: #fff;
        margin-bottom: 16px;
      }

      p {
        color: #fff;
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
      color: #fff;
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
      background-color: #42b883;
      padding: 16px;
      border-radius: 8px;
      color: #fff;
      font-size: 20px;
      text-transform: uppercase;
      transition: 0.4s;

      &:active {
        background-color: #3b8070;
      }
    }
  }
}

.movies-list {
  margin: 30px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
  gap: 5%;

  .movie {
    max-width: 50%;
    flex: 1 1 50%;
    padding: 16px 8px;
    .movie-link {
      display: flex;
      flex-direction: column;
      height: 100%;
      .product-image {
        position: relative;
        display: block;
        img {
          display: block;
          width: 100%;
          height: 275px;
          object-fit: cover;
        }
        .type {
          position: absolute;
          padding: 8px 16px;
          background-color: #42b883;
          color: #fff;
          bottom: 16px;
          left: 0px;
          text-transform: capitalize;
        }
      }
      .detail {
        background-color: #496583;
        padding: 16px 8px;
        flex: 1 1 100%;
        border-radius: 0px 0px 8px 8px;
        .year {
          color: #aaa;
          font-size: 14px;
        }
        h3 {
          color: #fff;
          font-weight: 600;
          font-size: 18px;
        }
      }
    }
  }
}
</style>
