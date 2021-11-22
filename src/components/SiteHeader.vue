<template>
  <header>
    <label for="chars">Type some characters to search a Movie/Serie: </label>
    <input v-model="entry" type="text" id="chars" name="chars" />
    <button @click="$emit('getAPI', entry)">Search!</button>
  </header>
</template>

<script>
export default {
  data() {
    return {
      entry: "",
    };
  },
  methods: {},
};
</script>

<style>
</style>