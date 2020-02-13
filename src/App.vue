<template>
<div id="app">
  <img alt="Vue logo" src="./assets/logo.png" />
  <h1>Love You! Stenie~</h1>
  <renderer msg="Welcome to my SVG plotter" />
</div>
</template>

<script>
import renderer from "./components/renderer.vue";

export default {
  name: "app",
  components: {
    renderer
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
