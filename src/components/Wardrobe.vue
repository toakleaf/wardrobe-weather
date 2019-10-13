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
    time: {
      type: Number,
      default: Date.now()
    },
    temp: {
      type: Number,
      default: 75
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
</style>

<template>
  <svg
    version="1.1"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    x="0px"
    y="0px"
    width="170px"
    height="500px"
    viewBox="0 0 170 500"
    enable-background="new 0 0 170 500"
    xml:space="preserve"
  >
    <umbrella v-if="conditions === 'Rain' || conditions === 'Drizzle' " />
    <model-body />
    <model-head />
    <flip-flops />
    <sandals />
    <flats />
    <shorts />
    <jeans />
    <rain-boots />
    <winter-boots />
    <flowy-pants />
    <tank-top />
    <t-shirt />
    <sweater />
    <mittens />
    <cowel-scarf />
    <rain-coat />
    <light-scarf />
    <winter-coat />
    <sun-glasses />
    <wind-hair />
    <stocking-hat />
  </svg>
</template>