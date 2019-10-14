<script>
import CowelScarf from "./wardrobe/CowelScarf.vue";
import Flats from "./wardrobe/Flats.vue";
import FlipFlops from "./wardrobe/FlipFlops.vue";
import FlowyPants from "./wardrobe/FlowyPants.vue";
import Jeans from "./wardrobe/Jeans.vue";
import LightScarf from "./wardrobe/LightScarf.vue";
import Mittens from "./wardrobe/Mittens.vue";
import ModelBody from "./wardrobe/ModelBody.vue";
import ModelHead from "./wardrobe/ModelHead.vue";
import RainBoots from "./wardrobe/RainBoots.vue";
import RainCoat from "./wardrobe/RainCoat.vue";
import Sandals from "./wardrobe/Sandals.vue";
import Shorts from "./wardrobe/Shorts.vue";
import StockingHat from "./wardrobe/StockingHat.vue";
import SunGlasses from "./wardrobe/SunGlasses.vue";
import Sweater from "./wardrobe/Sweater.vue";
import TankTop from "./wardrobe/TankTop.vue";
import TShirt from "./wardrobe/TShirt.vue";
import Umbrella from "./wardrobe/Umbrella.vue";
import WindHair from "./wardrobe/WindHair.vue";
import WinterBoots from "./wardrobe/WinterBoots.vue";
import WinterCoat from "./wardrobe/WinterCoat.vue";

export default {
  name: "Wardrobe",
  components: {
    CowelScarf,
    Flats,
    FlipFlops,
    FlowyPants,
    Jeans,
    LightScarf,
    Mittens,
    ModelBody,
    ModelHead,
    RainBoots,
    RainCoat,
    Sandals,
    Shorts,
    StockingHat,
    SunGlasses,
    Sweater,
    TankTop,
    TShirt,
    Umbrella,
    WindHair,
    WinterBoots,
    WinterCoat
  },
  props: {
    temp: {
      type: Number,
      default: 95
    },
    wind: {
      type: Number,
      default: 15
    },
    conditions: {
      type: String,
      default: "Clear"
    }
  }
};
</script>

<style scoped lang="scss">
svg {
  width: 80%;
  height: 100%;
}
</style>

<template>
  <svg
    version="1.1"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    x="0px"
    y="0px"
    viewBox="0 0 170 500"
    xml:space="preserve"
  >
    <umbrella v-if="conditions === 'Rain' || conditions === 'Drizzle' " />
    <model-body />
    <model-head />
    <flip-flops
      v-if="temp >= 90 && (conditions === 'Clear' || conditions === 'Cloudy' || conditions === 'Atmosphere')"
    />
    <sandals
      v-if="(temp > 75 && temp <= 90 && (conditions === 'Clear' || conditions === 'Cloudy' || conditions === 'Atmosphere'))"
    />
    <flats
      v-if="(temp > 40 && temp <= 75 && conditions !== 'Rain' && conditions !== 'Thunderstorm') || (temp > 75 && (conditions === 'Rain' && conditions === 'Thunderstorm' && conditions === 'Drizzle'))"
    />
    <shorts v-if="temp > 75" />
    <jeans v-if="temp <= 65" />
    <rain-boots
      v-if="(temp > 40 && temp <= 75 && (conditions === 'Rain') || conditions === 'Thunderstorm' || conditions === 'Drizzle')"
    />
    <winter-boots v-if="temp <= 40" />
    <flowy-pants v-if="temp > 65 && temp <= 75" />
    <tank-top v-if="(temp > 80 && conditions === 'Clear') || temp > 90" />
    <t-shirt v-if="(temp <= 90 && conditions !== 'Clear') || temp <= 80" />
    <sweater
      v-if="temp > 50 && temp <= 75 && conditions !== 'Rain' && conditions !== 'Thunderstorm' && conditions !== 'Drizzle'"
    />
    <mittens v-if="temp <= 40" />
    <cowel-scarf v-if="temp <= 50" />
    <rain-coat
      v-if="(temp > 40 && temp <= 75) && (conditions === 'Rain' || conditions === 'Thunderstorm' || conditions === 'Drizzle')"
    />
    <light-scarf v-if="temp > 50 && temp <= 60" />
    <winter-coat v-if="temp <= 50" />
    <sun-glasses v-if="conditions === 'Clear'" />
    <wind-hair v-if=" wind >= 10 " />
    <stocking-hat v-if="temp <= 40" />
  </svg>
</template>