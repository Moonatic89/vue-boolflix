<template>
  <main>
    <div class="movies">
      <h2 v-show="movies.length > 0">Movies</h2>
      <div class="container">
        <div class="row">
          <div class="card" v-for="movie in movies" :key="movie.id">
            <img
              class="cover"
              :src="generateCover(movie.poster_path)"
              @error="isImageBroken"
              alt=""
            />
          </div>
        </div>
      </div>

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
          <li>
            Voto:
            <span v-for="i in Math.ceil(movie.vote_average / 2)" v-bind:key="i">
              <i class="fas fa-star"></i>
            </span>
          </li>
          <li>
            Copertina:
            <img
              class="cover"
              :src="generateCover(movie.backdrop_path)"
              @error="isImageBroken"
              alt=""
            />
          </li>
          <li></li>
          <br />
        </ul>
      </li>
    </div>

    <!-- 
    <div class="movies">
      <h2 v-show="movies.length > 0">Movies</h2>
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

            </li>
            <li>
              Voto:
              <span
                v-for="i in Math.ceil(movie.vote_average / 2)"
                v-bind:key="i"
              >
                <i class="fas fa-star"></i>
              </span>
            </li>
            <li>
              Copertina:
              <img
                class="cover"
                :src="generateCover(movie.backdrop_path)"
                @error="isImageBroken"
                alt=""
              />
            </li>
            <li></li>
            <br />
          </ul>
        </li>
      </ol>
    </div> -->
    <!-- 
    <div class="series">
      <h2 v-show="series.length > 0">TV Series</h2>
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
            <li>
              Voto:
              <span
                v-for="i in Math.ceil(serie.vote_average / 2)"
                v-bind:key="i"
              >
                <i class="fas fa-star"></i>
              </span>
            </li>
            <li>
              <img
                class="cover"
                :src="generateCover(serie.backdrop_path)"
                @error="isImageBroken"
                alt=""
              />
            </li>
            <br />
          </ul>
        </li>
      </ol>
    </div> -->
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
      imageURL: "https://image.tmdb.org/t/p/",
      backdropSize: "w342",
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
    generateCover(cover) {
      return this.imageURL + this.backdropSize + cover;
    },
    isImageBroken(event) {
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

  .row {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;

    .card {
      padding: 2rem 2.5rem;
    }
  }

  .flag {
    width: 20px;
    height: 15px;
  }

  .cover {
    width: 300px;
  }
}
</style>