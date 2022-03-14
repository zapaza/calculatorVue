<template>
  <CCalculator />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CCalculator from "@/components/CCalculator.vue";

export default defineComponent({
  name: "App",
  components: { CCalculator },
});
</script>
