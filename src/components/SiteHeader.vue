<template>
  <header>
    <label for="chars">Type some characters to search a Movie:</label>
    <input v-model="entry" type="text" id="chars" name="chars" />
    <button @click="buildAPI">Search!</button>
  </header>
</template>

<script>
export default {
  data() {
    return {
      preFixed:
        "https://api.themoviedb.org/3/search/movie?api_key=f827a5bacdaf0b2436071ace43764985&language=en-US&query=",
      entry: "",
      sufFixed: "&page=1&include_adult=false",
      stringAPI: "",
    };
  },
  methods: {
    buildAPI() {
      this.stringAPI = this.preFixed + this.entry + this.sufFixed;
    },
  },
};
</script>

<style>
</style>