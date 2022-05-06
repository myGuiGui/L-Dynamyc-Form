<template>
  <div>
    <slot></slot>
    <kinput v-if="type == 'input'"></kinput>
    <ktext v-if="type == 'text'"></ktext>
    <knumberInput v-if="type == 'number-input'"></knumberInput>
  </div>
</template>

<script>
import kinput from "./functionMenu/input.vue";
import ktext from "./functionMenu/text.vue";
import knumberInput from "./functionMenu/numberInput.vue";
export default {
  props: {
    type: {
      type: [String, Number],
      default: "",
    },
  },
  components: {
    kinput,
    ktext,
    knumberInput,
  },
};
</script>

<style>
</style>