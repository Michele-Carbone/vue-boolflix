<template>
  <div id="app">
    <header>
      <h1>Boolflix</h1>
      <Search placeholder="Cerca un film.." @search="getResultsMovies" />
    </header>
    <main>
      <DisplayResults :combineResults="movies" :title="moviesTitle" />
      <DisplayResults :combineResults="series" :title="seriesTitle" />
    </main>
  </div>
</template>

<script>
import axios from "axios";
import Search from "@/components/Search.vue";
import DisplayResults from "@/components/DisplayResults.vue";
export default {
  name: "App",
  components: {
    Search,
    DisplayResults,
  },
  computed: {
    combineResults() {
      return [...this.movies, ...this.series];
    },
  },
  data() {
    return {
      movies: [],
      series: [],
      moviesTitle: "",
      seriesTitle: "",
      api: {
        key: "88b74998c2fb68ea366b7e3dba66a7ee",
        baseUrl: "https://api.themoviedb.org/3",
      },
    };
  },
  methods: {
    getResultsMovies(query) {
      if (!query) {
        this.movies = this.series = [];
        return;
      }

      this.takeApi(query, "search/movie", "movies");
      this.takeApi(query, "search/tv", "series");
      this.moviesTitle = "Film";
      this.seriesTitle = "Serie TV";
    },

    takeApi(query, endpoint, entity) {
      const params = {
        params: {
          query,
          api_key: this.api.key,
          language: "it-IT",
        },
      };

      axios.get(`${this.api.baseUrl}/${endpoint}`, params).then((res) => {
        this[entity] = res.data.results;
      });
    },
  },
};
</script>

<style lang="scss">
@import "scss/style.scss";
header {
  display: flex;
  background-color: $secondary-color;
  justify-content: space-around;
  align-items: center;
  padding: 20px 100px;

  h1 {
    color: $main-text-color;
  }
}
main {
  margin: 20px 0;
}
</style>
