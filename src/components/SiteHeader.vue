<template>
  <header>
    <nav>
      <div class="logoBox">
        <span class="logo">BOOLFLIX</span>
        <h2>Your new movie/TV series searchbar!</h2>
      </div>
      <div class="formGroup">
        <input v-model="entry" type="text" id="chars" name="chars" />
        <button @click="$emit('getAPI', entry)">Search!</button>
      </div>
    </nav>
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

<style lang="scss">
header {
  height: 60px;
  line-height: 60px;
  background-color: rgb(80, 80, 80);
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;

  nav {
    width: 75%;
    margin: auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .logoBox {
    display: flex;
    align-items: center;
  }

  .logo {
    color: crimson;
    text-shadow: -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000,
      1px 1px 0 #000;
    font-size: 2rem;
    font-weight: bolder;
    margin-right: 2rem;
  }
}
</style>