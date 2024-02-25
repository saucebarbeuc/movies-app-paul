<template>
    <div class="div_barre">
      <input v-model="searchQuery" type="text" placeholder="Rechercher" class="barre_recherche">
    </div>
  </template>
  
  <script>
    export default {
        data() {
            return {
                searchQuery: ''
            };
        },
        watch: {
            searchQuery(recherche) {
                this.$emit('searchMovieEmit', recherche);
            }
        }
    };
  </script>
  
  <style>
    .div_barre {
        display: flex;
        justify-content: center;
        margin: 60px;
    }
    
    .barre_recherche {
        color: aliceblue;
        padding: 10px;
        border: 2px solid #ccc;
        border-radius: 20px;
    }
  </style>
  