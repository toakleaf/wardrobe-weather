<template>
  <p>
    <span>&#x2316;</span>
    <input
      type="text"
      v-model="localValue"
      onfocus="this.select();"
      onmouseup="return false;"
      :size=" localValue && localValue.length > 7 ? localValue.length : 7"
      @blur="$emit('updateLocation', localValue)"
      @keyup.enter="$event.target.blur()"
    />
  </p>
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
p input {
  border: none;
  display: inline;
  font-family: inherit;
  font-size: inherit;
  padding: none;
  text-align: center;
  background: transparent;
}
p span {
  font-size: 150%;
}
</style>
