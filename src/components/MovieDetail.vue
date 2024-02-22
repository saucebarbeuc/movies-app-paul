<template>
    <div v-if="movie">
      <v-dialog v-model="dialog" max-width="600px">
        <v-card>
          <v-row>
           
            <v-col>
              <v-img :src="photopath + movie.poster_path" ></v-img>
            </v-col>
        
            <v-col>
              <v-card-text>
                <div>{{ movie.title }}</div>
                <v-rating v-model="movie.vote_average"></v-rating>
                <div>{{ movie.production_companies.join(', ') }}</div>
                <div>{{ movie.overview }}</div>
              </v-card-text>
            </v-col>
          </v-row>
        
          <v-card-actions class="close-button">
            <v-btn @click="closeDetail">Close</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import config from '../config.json';
  
  export default {
    name: 'MovieDetail',
    props: {
      movieId: {
        type: Number,
        required: true
      }
    },
    data() {
      return {
        movie: null,
        dialog: true,
        photopath: ''
      };
    },
    created() {
      axios.get(`${config.url.movie_detail}/${this.movieId}`, {
        headers: {
          'Authorization': `Bearer ${config.api_key}`
        }
      })
      .then(response => {
        this.photopath = config.url.photo_path;
        this.movie = response.data;
      })
      .catch(error => {
        console.error('Error fetching movie details:', error);
      });
    },
    methods: {
      closeDetail() {
        this.$emit('close');
      }
    }
  };
  </script>
  
  <style >
  .close-button {
    justify-content: flex-end;
  }
  
  </style>
  