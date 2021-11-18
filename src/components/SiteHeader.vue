<template>
  <header>
    <label for="chars">Type some characters to search a Movie:</label>
    <input v-model="entry" type="text" id="chars" name="chars" />
    <button @click="buildAPI(entry)">Search!</button>
  </header>
</template>

<script>
export default {
  data() {
    return {
      preFixed: "",
      entry: "",
      sufFixed: "",
      stringAPI: "",
    };
  },
  methods: {
    buildApi() {
      this.stringAPI = "";
    },
  },
};
</script>

<style>
</style>