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
              v-if="generateFlag(movie.original_language) != false"
              :src="generateFlag(movie.original_language)"
              alt=""
            />
            <span v-else>
              <strong>{{ movie.original_language }}</strong>
            </span>
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
import axios from "axios";
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
      switch (flag) {
        case "en":
          flag = "gb";
          break;
        case "ja":
          flag = "jp";
          break;
        default: {
          const flagUrlCheck = this.flagURL + flag + this.formatPNG;

          axios
            .get(flagUrlCheck)
            .then((r) => {
              console.log(r);
            })
            .catch((err) => {
              if (err == "404") {
                return false;
              }
            });

          return this.flagURL + flag + this.formatPNG;
        }
      }
    },
  },
};
</script>



<style lang="scss">
.flag {
  width: 20px;
  height: 15px;
}
</style>