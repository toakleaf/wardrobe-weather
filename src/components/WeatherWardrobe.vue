<template>
  <div>
    <wardrobe />
  </div>
</template>

<script>
import Wardrobe from "./Wardrobe.vue";

export default {
  name: "HelloWorld",
  components: {
    Wardrobe
  },
  props: {
    msg: String
  }
};
</script>

<style scoped lang="scss">
</style>
