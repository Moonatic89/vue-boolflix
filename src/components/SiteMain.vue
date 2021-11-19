<template>
  <main>
    <h1></h1>
    <ol>
      <li v-for="movie in movies" :key="movie.id">
        <ul>
          <li>Titolo: {{ movie.title }}</li>
          <li>Titolo Originale: {{ movie.original_title }}</li>
          <li>
            Lingua:
            <img
              class="flag"
              :src="generateFlag(movie.original_language)"
              alt=""
            />
          </li>
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
      flagURL: "https://flagcdn.com/256x192/",
      formatPNG: ".png",
      flag: "",
      //   importedAPI: [],
    };
  },
  methods: {
    generateFlag(flag) {
      return this.flagURL + flag + this.formatPNG;
    },
  },
};
</script>



<style lang="scss">
.flag {
  background-color: red;
}
</style>