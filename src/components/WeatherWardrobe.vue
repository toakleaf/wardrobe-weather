<template>
  <div
    class="weather-wardrobe"
    :style=" {'background-image': `linear-gradient(to bottom right, ${bgColor1}, ${bgColor2})` }"
  >
    <Loading v-if="loading" />
    <wardrobe
      v-if="!loading && !error"
      :wind="forecastWind"
      :temp="forecastTemp"
      :conditions="forecastConditions"
    />
  </div>
</template>

<script>
import Wardrobe from "./Wardrobe.vue";
import Loading from "./Loading.vue";
import axios from "axios";

export default {
  name: "WeatherWardrobe",
  components: {
    Wardrobe,
    Loading
  },
  data: function() {
    return {
      bgColor1: "blue",
      bgColor2: "green",
      conditionsList: [
        "Thunderstorm",
        "Snow",
        "Rain",
        "Drizzle",
        "Atmosphere",
        "Clouds",
        "Clear"
      ],
      coords: null,
      city: "Boston",
      country: "USA",
      loading: true,
      forecastTemp: null,
      forecastWind: null,
      forecastConditions: null,
      error: null
    };
  },
  methods: {
    getLocation: function() {
      return new Promise(function(resolve, reject) {
        navigator.geolocation.getCurrentPosition(resolve, reject);
      });
    },
    getforecast: function() {
      // forecast is an average of next 6 hours so you can plan your day.
      this.loading = true;
      axios
        .get("https://api.openweathermap.org/data/2.5/forecast", {
          params: {
            ...(this.coords
              ? { lat: this.coords.latitude, lon: this.coords.longitude }
              : { q: `${this.city},${this.country}` }),
            units: "imperial",
            cnt: 2,
            appid: process.env.VUE_APP_WEATHER_API_KEY
          }
        })
        .then(res => {
          if (res.data.cod !== "200")
            throw new Error("Failed to fetch weather data from API");
          const temps = res.data.list.map(i => i.main.temp);
          const winds = res.data.list.map(i => i.wind.speed);
          const weather = res.data.list.map(i =>
            this.conditionsList.indexOf(i.weather[0].main)
          );

          this.forecastTemp = temps.reduce((a, b) => a + b, 0) / 2;
          this.forecastWind = winds.reduce((a, b) => a + b, 0) / 2;

          // Always dress for worst weather
          this.forecastConditions = this.conditionsList[Math.min(...weather)];
        })
        .catch(err => {
          this.error = err;
        })
        .then(res => {
          this.loading = false;
        });
    }
  },
  mounted() {
    this.getLocation()
      .then(pos => {
        this.coords = pos.coords;
        this.getforecast();
      })
      .catch(err => {
        console.error(err.message);
      });
  }
};
</script>

<style scoped lang="scss">
.weather-wardrobe {
  height: 100%;
  width: 100%;
  margin: 0;
  display: inline-flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}
</style>
