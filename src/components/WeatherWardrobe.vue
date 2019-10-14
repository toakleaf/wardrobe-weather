<template>
  <div
    class="weather-wardrobe"
    :style=" {'background-image': `linear-gradient(to bottom right, ${bgColor1}, ${bgColor2})` }"
  >
    <wardrobe />
  </div>
</template>

<script>
import Wardrobe from "./Wardrobe.vue";

export default {
  name: "WeatherWardrobe",
  components: {
    Wardrobe
  },
  data: function() {
    return {
      bgColor1: "blue",
      bgColor2: "green"
    };
  },
  mounted() {
    console.log(process.env.VUE_APP_WEATHER_API_KEY);
  }
};
</script>

<style scoped lang="scss">
.weather-wardrobe {
  min-height: 100%;
  margin: 0;
}
</style>
