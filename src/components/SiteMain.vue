<template>
  <main>
    <h1></h1>
    <ol>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ol>
  </main>
</template>

<script>
import axios from "axios";
export default {
  props: {
    stringEntry: String,
  },

  data() {
    return {
      importedAPI: [],
      completeAPIString: this.getAPI,
      preFixed:
        "https://api.themoviedb.org/3/search/movie?api_key=f827a5bacdaf0b2436071ace43764985&language=en-US&query=",
      sufFixed: "&page=1&include_adult=false",
    };
  },
  computed: {
    getAPI() {
      return this.preFixed + this.stringAPI + this.sufFixed;
    },
  },
  mounted() {
    if (this.stringAPI != "") {
      axios.get(this.stringAPI).then((r) => {
        this.importedAPI = r.data.response;
      });
    }
  },
};
</script>

<style>
</style>