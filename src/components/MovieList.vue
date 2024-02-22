<template>
    <div>
      <h2>Movie List</h2>
      <ul class="movie-list">
        <li v-for="result in results" :key="result.id" class="movie-item">
          <div @click="showMovieDetail(result.id)">
            <img :src="photopath + result.poster_path" class="movie-poster" />
            <p class="movie-title">{{ result.title }}</p>
          </div>
        </li>
      </ul>
      <MovieDetail v-if="selectedMovieId !== null" :movieId="selectedMovieId" @close="resetSelectedMovie"></MovieDetail>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import config from '../config.json';
  import MovieDetail from './MovieDetail.vue';
  
  export default {
    name: 'MovieList',
    components: {
      MovieDetail
    },
    data() {
      return {
        results: [],
        photopath: '',
        selectedMovieId: null
      };
    },
    created() {
      axios.get(config.url.movie_list, {
        headers: {
          'Authorization': `Bearer ${config.api_key}`
        }
      })
      .then(response => {
        this.photopath = config.url.photo_path;
        this.results = response.data.results;
      })
      .catch(error => {
        console.error('Error fetching movies:', error);
      });
    },
    methods: {
      showMovieDetail(movieId) {
        this.selectedMovieId = movieId;
      },
      resetSelectedMovie() {
        this.selectedMovieId = null;
      }
    }
  };
  </script>
  
  <style scoped>
  .movie-list {
    list-style-type: none;
    display: flex;
    flex-wrap: wrap;
  }
  
  .movie-item {
    margin: 10px;
    width: full;
    height: full;
    text-align: center;
  }
  
  .movie-poster {
    margin: 10px;
    width: 200px;
    height: 300px;
  }
  
  .movie-title {
    margin: 3px;
    font-size: 14px;
  }
  </style>
  