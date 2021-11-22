<template>
  <main>
    <div class="movies">
      <div class="container">
        <h2 v-show="movies.length > 0">Movies</h2>
        <div class="row">
          <div class="card" v-for="movie in movies" :key="movie.id">
            <div class="imageBox">
              <div class="overlay">
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
                    <span
                      v-for="i in Math.ceil(movie.vote_average / 2)"
                      v-bind:key="i"
                    >
                      <i class="fas fa-star"></i>
                    </span>
                  </li>

                  <div class="member" v-for="i in 5" :key="i">
                    <span>
                      {{ generateCastMembers(movie.id, i) }}
                    </span>
                  </div>

                  <li>
                    {{ movie.overview }}
                  </li>
                </ul>
              </div>
              <img
                class="cover"
                :src="generateCover(movie.poster_path)"
                @error="isImageBroken"
                alt=""
              />
            </div>
            <h2>{{ movie.title }}</h2>
          </div>
        </div>

        <h2 v-show="series.length > 0">TV Series</h2>
        <div class="row">
          <div class="card" v-for="serie in series" :key="serie.id">
            <div class="imageBox">
              <div class="overlay">
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
                    {{ serie.overview }}
                  </li>
                  <li></li>
                </ul>
              </div>
              <img
                class="cover"
                :src="generateCover(serie.poster_path)"
                @error="isImageBroken"
                alt=""
              />
            </div>
            <h2>{{ serie.name }}</h2>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>


<script>
import axios from "axios";
export default {
  props: {
    movies: Array,
    series: Array,
  },

  data() {
    return {
      imageURL: "https://image.tmdb.org/t/p/",
      castURL: "https://api.themoviedb.org/3/movie/",
      castMember: "",
      castArr: [],
      apiKey: "/credits?api_key=f827a5bacdaf0b2436071ace43764985",

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

    generateCastMembers(entryID, index) {
      axios.get(this.castURL + entryID + this.apiKey).then((r) => {
        console.log(r.data.cast[index - 1].name);
        this.castMember = r.data.cast[index - 1].name;
      });
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
  background-color: rgb(200, 197, 197);
  display: flex;
  padding: 0 5rem;

  .row {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;

    .card {
      // padding: 2rem 2.5rem;

      .imageBox {
        position: relative;

        .overlay {
          margin: 0.5rem;
          padding: 0.5rem;
          border-radius: 15px;
          position: absolute;
          background: rgb(0, 0, 0);
          background: linear-gradient(
            180deg,
            rgba(0, 0, 0, 1) 0%,
            rgba(71, 71, 71, 1) 72%,
            rgba(0, 212, 255, 0) 100%
          );
          color: white;
          width: 330px;
          height: 512px;
          overflow-y: auto;

          ul {
            list-style: none;

            li {
              padding: 0.25rem 0.25rem;
            }
          }

          i {
            color: yellow;
          }
        }
        img {
          position: relative;
          z-index: 1;
          background-color: black;
        }

        .overlay:hover {
          z-index: 2;
        }

        img:hover {
          z-index: -1;
        }
      }
      h2 {
        text-align: center;
      }
    }
  }

  .flag {
    width: 20px;
    height: 15px;
  }

  .cover {
    width: 342px;
    height: 512px;
    object-fit: contain;
    object-position: top;
  }
}
</style>