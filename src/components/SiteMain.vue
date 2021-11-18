<template>
  <main>
    <h1></h1>
    <ol>
      <li v-for="movie in movies" :key="movie.id">
        <ul>
          <li>Titolo: {{ movie.title }}</li>
          <li>Titolo Originale: {{ movie.original_title }}</li>
          <li>Lingua: {{ movie.original_language }}</li>
          <li>Voto: {{ movie.vote_average }}</li>
          <br />
        </ul>
      </li>

      <ul></ul>
    </ol>
  </main>
</template>


<script>
export default {
  props: {
    movies: Array,
  },

  data() {
    return {
      //   importedAPI: [],
    };
  },
};
</script>



<style>
</style>