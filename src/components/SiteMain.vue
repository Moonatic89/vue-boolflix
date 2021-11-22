<template>
  <main>
    <div class="movies">
      <h2>Movies</h2>
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
                @error="isImageBroken"
                alt=""
              />

              <!-- <img v-else class="flag" src="../assets/error.png" alt="" /> -->
            </li>
            <li>Voto: {{ movie.vote_average }}</li>
            <br />
          </ul>
        </li>

        <ul></ul>
      </ol>
    </div>

    <div class="series">
      <h2>TV Series</h2>
      <ol>
        <li v-for="serie in series" :key="serie.id">
          <ul>
            <li>Titolo: {{ serie.name }}</li>
            <li>Titolo Originale: {{ serie.original_name }}</li>
            <li>
              Lingua:
              <img
                class="flag"
                :src="generateFlag(serie.original_language)"
                @error="isImageBroken"
                alt=""
              />
            </li>
            <li>Voto: {{ serie.vote_average }}</li>
            <br />
          </ul>
        </li>

        <ul></ul>
      </ol>
    </div>
  </main>
</template>


<script>
// import axios from "axios";
export default {
  props: {
    movies: Array,
    series: Array,
  },

  data() {
    return {
      brokenURL: "assets/error.png",
      flagURL: "https://flagcdn.com/256x192/",
      formatPNG: ".png",
      flag: "",
    };
  },
  methods: {
    generateFlag(flag) {
      switch (flag) {
        case "en":
          flag = "gb";
          break;
        case "ja":
          flag = "jp";
          break;
      }

      return this.flagURL + flag + this.formatPNG;
    },
    isImageBroken(event) {
      //console.log(event);
      event.target.src = event.target.baseURI + this.brokenURL;
      console.log(event);
    },
  },
};
</script>



<style lang="scss">
main {
  display: flex;
  padding: 0 5rem;

  .flag {
    width: 20px;
    height: 15px;
  }
}
</style>