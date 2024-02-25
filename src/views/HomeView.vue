<template>
  <div>
    <div class="titre">
      <h1>PBStream</h1>
    </div>
    <MovieSearch @searchMovieEmit="setSearchMovie"></MovieSearch>
    <MovieList :searchQuery="searchQuery" @showMovieDetailEmit="showMovieDetail"></MovieList>
    <MovieDetail v-if="selectedMovieId !== null" :movieId="selectedMovieId" @close="resetSelectedMovie"></MovieDetail>
  </div>
</template>

<script>
  import MovieList from '../components/MovieList.vue';
  import MovieDetail from '../components/MovieDetail.vue';
  import MovieSearch from '../components/movieSearch.vue';

  export default {
    name: 'HomeView',
    components: {
      MovieList,
      MovieDetail,
      MovieSearch
    },
    data() {
      return {
        selectedMovieId: null,
        searchQuery: '',
      };
    },
    methods: {
      showMovieDetail(movieId) {
        this.selectedMovieId = movieId;
      },
      resetSelectedMovie() {
        this.selectedMovieId = null;
      },
      setSearchMovie(query) {
        this.searchQuery = query;
      }
    }
  };
</script>

<style>
  .titre{
    padding: 10px;
    color: rgb(0, 202, 0);
  }
</style>
