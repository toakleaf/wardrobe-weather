<template>
  <div>
    <div class="weather-wardrobe">
      <div class="row">
        <Loading v-if="loading && !error" class="row-item" />

        <wardrobe
          v-if="!loading && !error"
          :wind="forecastWind"
          :temp="forecastTemp"
          :conditions="forecastConditions[0]"
          class="row-item"
        />

        <info-pane
          v-if="!loading"
          class="row-item"
          :temp="forecastTemp"
          :wind="forecastWind"
          :conditions="forecastConditions[0]"
          :city="city"
          :country="country"
          :error="error"
          @updateLocation="updateLocation"
        />
      </div>
    </div>
    <transition-group name="fade">
      <div
        class="bg"
        v-for="c in forecastConditions"
        :key="c ? c : 0"
        :class="c ? c.toLowerCase() : ''"
      ></div>
    </transition-group>
  </div>
</template>

<script>
import Wardrobe from "./Wardrobe.vue";
import InfoPane from "./InfoPane.vue";
import Loading from "./Loading.vue";
import axios from "axios";

export default {
  name: "WeatherWardrobe",
  components: {
    Wardrobe,
    InfoPane,
    Loading
  },
  data: function() {
    return {
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
      country: "US",
      loading: true,
      forecastTemp: null,
      forecastWind: null,
      forecastConditions: ["Atmosphere"],
      error: null
    };
  },
  methods: {
    getLocation: function() {
      return new Promise((resolve, reject) => {
        if (!navigator.geolocation)
          reject("Geolocation is not supported by this browser.");
        let options = { timeout: 5000 };
        navigator.geolocation.getCurrentPosition(resolve, reject, options);
      });
    },
    getForecast: function() {
      // forecast is an average of next 6 hours so you can plan your day.
      this.loading = true;
      this.error = null;
      axios
        .get("https://api.openweathermap.org/data/2.5/forecast", {
          params: {
            ...(this.coords
              ? { lat: this.coords.latitude, lon: this.coords.longitude }
              : { q: `${this.city}${this.country ? "," + this.country : ""}` }),
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
          this.forecastConditions = [this.conditionsList[Math.min(...weather)]];

          this.city = res.data.city.name;
          this.country = res.data.city.country;
        })
        .catch(err => {
          this.error = err;
          console.error(err);
        })
        .then(res => {
          this.loading = false;
        });
    },
    updateLocation: function(loc) {
      if (!loc) return;

      const locStrings = loc.split(",").map(s => s.trim());

      if (
        this.city === locStrings[0] &&
        (locStrings.length < 2 || locStrings[1] === this.country)
      )
        return;

      this.coords = null;
      this.city = locStrings[0];
      this.country = locStrings.length > 1 ? locStrings[1] : null;
      this.getForecast();
    }
  },
  mounted() {
    this.getLocation()
      .then(pos => {
        this.coords = pos.coords;
      })
      .catch(err => {
        console.error(err);
      })
      .then(() => {
        this.getForecast();
      });
  }
};
</script>

<style scoped lang="scss">
.weather-wardrobe {
  height: 100%;
  width: 100%;
  margin: 0;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 1;
  display: inline-flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}
.row {
  border-radius: 3rem;
  background-image: linear-gradient(
    to top right,
    rgba(255, 255, 255, 0),
    rgba(255, 255, 255, 0.3)
  );
  display: inline-flex;
  flex-flow: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}
.row-item {
  height: 90vh;
  width: 45vw;
}
.thunderstorm {
  background-image: linear-gradient(to bottom right, #7c3fe5, #d8abd1);
}
.snow {
  background-image: linear-gradient(to bottom right, #6e88b8, #aacdfa);
}
.rain {
  background-image: linear-gradient(to bottom right, #a2bae1, #254d94);
}
.drizzle {
  background-image: linear-gradient(to bottom right, #a3c8fb, #efe8e0);
}
.atmosphere {
  background-image: linear-gradient(to bottom right, #e8e8e8, #c1cfd8);
}
.clouds {
  background-image: linear-gradient(to bottom right, #35dfff, #1781ff);
}
.clear {
  background-image: linear-gradient(to bottom right, #8bf3d8, #4eddf6);
}
.bg {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  margin: 0;
  z-index: -1;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: 2s;
}
</style>
