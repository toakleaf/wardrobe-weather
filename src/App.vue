<template>
  <div id="app">
    <WeatherWardrobe msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import WeatherWardrobe from "./components/WeatherWardrobe.vue";

export default {
  name: "app",
  components: {
    WeatherWardrobe
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
