<template>
  <div>
    <MovieList @showDetail="showMovieDetail"></MovieList>
    <MovieDetail v-if="selectedMovieId" :movieId="selectedMovieId" @close="closeMovieDetail"></MovieDetail>
  </div>
</template>

<script>
import MovieList from './components/MovieList.vue';
import MovieDetail from './components/MovieDetail.vue';

export default {
  name: 'App',
  el: '#app',
  components: { MovieList, MovieDetail },
  data() {
    return {
      selectedMovieId: null
    };
  },
  methods: {
    showMovieDetail(movieId) {
      this.selectedMovieId = movieId;
    },
    closeMovieDetail() {
      this.selectedMovieId = null;
    }
  }
};
</script>

<style lang="scss">
body{
  color: aliceblue;
  background-color: rgb(41, 41, 41);
}
</style>
