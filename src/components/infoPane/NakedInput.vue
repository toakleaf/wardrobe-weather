<template>
  <span>
    <span class="xhairs">&#x2316;</span>
    <input
      type="text"
      v-model="localValue"
      onfocus="this.select();"
      onmouseup="return false;"
      :size=" localValue && localValue.length > 7 ? localValue.length : 7"
      @blur="$emit('updateLocation', localValue)"
      @keyup.enter="$event.target.blur()"
    />
  </span>
</template>

<script>
export default {
  name: "NakedInput",
  props: {
    value: {
      type: String
    }
  },
  data: function() {
    return {
      localValue: null
    };
  },
  watch: {
    value: function(v) {
      this.localValue = v;
    }
  },
  mounted() {
    this.localValue = this.value;
  }
};
</script>

<style lang="scss" scoped>
input {
  border: none;
  display: inline;
  font-family: inherit;
  font-size: inherit;
  padding: none;
  text-align: center;
  background: transparent;
}
.xhairs {
  font-size: 150%;
}
</style>
