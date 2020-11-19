<template>
  <div id="app">
    <Movies></Movies>
  </div>
</template>

<script>
import Movies from "./components/Movies";

export default {
  name: "App",
  components: {
    Movies,
  },
};
</script>

<style>
body {
  background: black;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0 auto;
  width: 400px;
  background: black;
  padding: 20px;
  color: white;
}
</style>
