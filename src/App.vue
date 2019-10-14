<template>
  <div id="app">
    <WeatherWardrobe />
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
  height: 100%;
  margin: 0;
}
</style>
