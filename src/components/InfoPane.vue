<template>
  <div class="info-pane">
    <svg viewBox="0 0 60 18" v-if="error">
      <text
        x="50%"
        y="50%"
        dominant-baseline="middle"
        text-anchor="middle"
        font-size="3"
      >Could not retrieve data for location.</text>
    </svg>
    <svg viewBox="0 0 60 18" v-if="!error">
      <text
        x="50%"
        y="50%"
        dominant-baseline="middle"
        text-anchor="middle"
      >{{Math.round(temp)}}&deg;</text>
    </svg>
    <svg viewBox="0 0 60 18" v-if="!error">
      <text
        x="50%"
        y="50%"
        dominant-baseline="middle"
        text-anchor="middle"
        font-size="10"
      >{{conditions}}</text>
    </svg>
    <svg viewBox="0 0 60 18" v-if="!error">
      <text
        x="50%"
        y="50%"
        dominant-baseline="middle"
        text-anchor="middle"
        font-size="5"
      >{{Math.round(wind)}} mph Wind</text>
    </svg>
    <naked-input :value="locationString" @updateLocation="$emit('updateLocation', $event)" />
  </div>
</template>

<script>
import NakedInput from "./infoPane/NakedInput.vue";

export default {
  name: "InfoPane",
  components: {
    NakedInput
  },
  props: {
    temp: {
      type: Number
    },
    wind: {
      type: Number
    },
    conditions: {
      type: String
    },
    city: {
      type: String
    },
    country: {
      type: String
    },
    error: {
      type: Error
    }
  },
  computed: {
    locationString: function() {
      return `${this.city}${this.country ? ", " + this.country : ""}`;
    }
  }
};
</script>

<style lang="scss" scoped>
.info-pane {
  height: 100%;
  padding: 1em 0 1em 0;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
}
p input {
  border: none;
  display: inline;
  font-family: inherit;
  font-size: inherit;
  padding: none;
}
</style>
