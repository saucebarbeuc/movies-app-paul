<template>
    <div>
      <ul class="movie-list">
        <li v-for="movie in movieFiltered" :key="movie.id" class="movie-item">
          <div @click="showMovieDetail(movie.id)">
            <img :src="photopath + movie.poster_path" class="movie-poster" />
            <p class="movie-title">{{ movie.title }}</p>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
    import axios from 'axios';
    import config from '../config.json';
    import _ from 'lodash';
    
    export default {
        name: 'MovieList',
        props: {
            searchQuery: String,
        },
        data() {
            return {
                results: [],
                photopath: '',
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
                console.error('Erreur lors de la récupération des films: ', error);
            });
        },
        computed: {
            movieFiltered() {
                if (!this.searchQuery) {
                    return this.results;
                } else {
                    return _.filter(this.results, movie => {
                        return movie.title.toLowerCase().includes(this.searchQuery.toLowerCase());
                    });
                }
            }
        },
        methods: {
            showMovieDetail(movieId) {
                this.$emit('showMovieDetailEmit', movieId);
            }
        }
    };
  </script>

  <style>
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
        font-size: 18px;
        text-overflow: ellipsis;
        max-width: 200px;
        overflow: hidden;
        white-space: nowrap;
    }
  </style>
  