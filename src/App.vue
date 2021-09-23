<template>
  <div id="app">
    <header>
      <Search placeholder="Cerca un film.." @search="getMovies" />
    </header>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
export default {
  name: "App",
  components: { Search },
  methods: {
    getMovies(query) {
      console.log(query);
    },
  },
};
</script>

<style lang="scss">
</style>
