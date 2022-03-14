<template>
  <div class="calculator">
    <div class="calculator__mode">
      <CSwitch />
    </div>
    <div class="calculator__display">
      <div class="calculator__display-history">{{ history }}</div>
      <div class="calculator__display-sum">{{ sum }}</div>
    </div>
    <div class="calculator__buttons">
      <CButton value="C" type="medium"></CButton>
      <CButton type="medium"></CButton>
      <CButton value="%" type="medium"></CButton>
      <CButton value="÷" type="high"></CButton>

      <CButton value="7" type="low"></CButton>
      <CButton value="8" type="low"></CButton>
      <CButton value="9" type="low"></CButton>
      <CButton value="×" type="high"></CButton>

      <CButton value="4" type="low"></CButton>
      <CButton value="5" type="low"></CButton>
      <CButton value="6" type="low"></CButton>
      <CButton value="–" type="high"></CButton>

      <CButton value="1" type="low"></CButton>
      <CButton value="2" type="low"></CButton>
      <CButton value="3" type="low"></CButton>
      <CButton value="+" type="high"></CButton>

      <CButton value="." type="low"></CButton>
      <CButton value="0" type="low"></CButton>
      <CButton type="low"></CButton>
      <CButton value="=" type="high"></CButton>
    </div>
  </div>
</template>

<script>
import CButton from "@/components/CButton.vue";
import CSwitch from "@/components/CSwitch.vue";
import { ref } from "vue";

export default {
  name: "CCalculator",
  components: { CSwitch, CButton },
  setup() {
    const sum = ref("");
    const history = ref("");

    return {
      sum,
      history,
    };
  },
};
</script>
