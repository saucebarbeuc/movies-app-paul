<template>
  <div id="app">
    <HomeView></HomeView>
  </div>
</template>

<script>
  import HomeView from './views/HomeView.vue';

  export default {
    name: 'App',
    components: {
      HomeView
    }
  };
</script>

<style>
  body {
    color: aliceblue;
    background-color: rgb(41, 41, 41);
  }
</style>
