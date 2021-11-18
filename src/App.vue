<template>
  <div id="app">
    <SiteHeader @getAPI="buildAPI" />
    <SiteMain :stringAPI="stringAPI" />

    <!-- <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import SiteHeader from "./components/SiteHeader.vue";
import SiteMain from "./components/SiteMain.vue";

export default {
  name: "App",
  components: {
    SiteHeader,
    SiteMain,
    // HelloWorld,
  },
  data() {
    return {
      preFixed:
        "https://api.themoviedb.org/3/search/movie?api_key=f827a5bacdaf0b2436071ace43764985&language=en-US&query=",
      sufFixed: "&page=1&include_adult=false",
      stringAPI: "",
    };
  },
  methods: {
    buildAPI(entry) {
      this.stringAPI = this.preFixed + entry + this.sufFixed;
    },
  },
};
</script>

<style lang="scss">
// #app {
//   font-family: Avenir, Helvetica, Arial, sans-serif;
//   -webkit-font-smoothing: antialiased;
//   -moz-osx-font-smoothing: grayscale;
//   text-align: center;
//   color: #2c3e50;
//   margin-top: 60px;
// }
</style>
