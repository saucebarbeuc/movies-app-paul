<template>
    <div v-if="movie">
      <v-dialog v-model="dialog" max-width="600px">
        <v-card>
          <div class="dialog-content">
            <v-img class="dialog-image" :src="photopath + movie.poster_path" ></v-img>
            <div class="dialog-title">{{ movie.title }}</div>
            <div class="dialog-description">{{ movie.overview }}</div>
            <div class="bouton_fermer">
              <v-btn @click="closeDetail">Fermer</v-btn>
            </div>
          </div>
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
            }
        },
        data() {
            return {
                movie: null,
                dialog: true,
                photopath: '',
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
                console.error('Erreur lors de la récupération des films: ', error);
            });
        },
        methods: {
            closeDetail() {
                this.dialog = false; 
                this.$emit('close');
            }
        }
    };
  </script>
  
  <style>
    .dialog-content {
        padding: 20px;
    }

    .dialog-image {
        width: 200px;
    }

    .dialog-title {
        font-size: 24px;
        margin-bottom: 10px;
    }

    .dialog-description {
        margin-bottom: 20px;
    }

    .bouton_fermer {
        margin-top: 20px;
        text-align: right;
    };

    .bouton_fermer button {
        padding: 10px 20px;
        background-color: #333;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
</style>
