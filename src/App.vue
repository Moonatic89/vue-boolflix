<template>
  <div id="app">
    <SiteHeader @getAPI="getEntry" />
    <SiteMain :movies="importedMovies" :series="importedSeries" />

    <!-- <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
import SiteHeader from "./components/SiteHeader.vue";
import SiteMain from "./components/SiteMain.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    SiteHeader,
    SiteMain,
  },
  data() {
    return {
      stringEntry: "",
      importedMovies: [],
      importedSeries: [],

      siteURL: "https://api.themoviedb.org/3/search/",
      searchMovie: "movie",
      searchTv: "tv",

      preFixed:
        "https://api.themoviedb.org/3/search/movie?api_key=f827a5bacdaf0b2436071ace43764985&language=en-US&query=",
      preFixedSeries:
        "https://api.themoviedb.org/3/search/tv?api_key=f827a5bacdaf0b2436071ace43764985&language=en-US&query=",

      sufFixed: "&page=1&include_adult=false",
    };
  },
  methods: {
    getEntry(entry) {
      this.stringEntry = this.preFixed + entry + this.sufFixed;
      axios.get(this.stringEntry).then((r) => {
        this.importedMovies = r.data.results;
      });

      this.stringEntry = this.preFixedSeries + entry + this.sufFixed;
      axios.get(this.stringEntry).then((r) => {
        this.importedSeries = r.data.results;
      });
    },
  },
};
</script>

<style lang="scss">
@import "./assets/scss/common.scss";
</style>
