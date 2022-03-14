<template>
  <button
    class="calculator-button"
    type="button"
    :class="{
      'calculator-button--low': type === 'low',
      'calculator-button--medium': type === 'medium',
      'calculator-button--high': type === 'high',
    }"
    @click.prevent="$emit('click-button')"
  >
    <template v-if="value">{{ value }}</template>
    <slot v-else />
  </button>
</template>

<script lang="ts">
export default {
  name: "CButton",
  props: {
    type: {
      type: String,
      default: "low",
    },
    value: {
      type: String,
    },
  },
};
</script>
