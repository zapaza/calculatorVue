<template>
  <div class="calculator">
    <div class="calculator__mode">
      <CSwitch />
    </div>
    <div class="calculator__display">
      <div v-if="selectedOperation" class="calculator__display-history">
        {{ prevNum }} {{ selectedOperation }} {{ currentNum }}
      </div>
      <div class="calculator__display-sum">{{ currentNum }}</div>
    </div>
    <div class="calculator__buttons">
      <CButton value="C" type="medium" @click-button="pressed('c')"></CButton>
      <CButton type="medium" @click-button="negateValue"></CButton>
      <CButton value="%" type="medium" @click-button="pressed('%')"></CButton>
      <CButton value="÷" type="high" @click-button="pressed('/')"></CButton>

      <CButton value="7" type="low" @click-button="pressed('7')"></CButton>
      <CButton value="8" type="low" @click-button="pressed('8')"></CButton>
      <CButton value="9" type="low" @click-button="pressed('9')"></CButton>
      <CButton value="×" type="high" @click-button="pressed('*')"></CButton>

      <CButton value="4" type="low" @click-button="pressed('4')"></CButton>
      <CButton value="5" type="low" @click-button="pressed('5')"></CButton>
      <CButton value="6" type="low" @click-button="pressed('6')"></CButton>
      <CButton value="–" type="high" @click-button="pressed('-')"></CButton>

      <CButton value="1" type="low" @click-button="pressed('1')"></CButton>
      <CButton value="2" type="low" @click-button="pressed('2')"></CButton>
      <CButton value="3" type="low" @click-button="pressed('3')"></CButton>
      <CButton value="+" type="high" @click-button="pressed('+')"></CButton>

      <CButton value="." type="low" @click-button="pressed('.')"></CButton>
      <CButton value="0" type="low" @click-button="pressed('0')"></CButton>
      <CButton type="low" @click-button="deleteValue"></CButton>
      <CButton value="=" type="high" @click-button="pressed('=')"></CButton>
    </div>
  </div>
</template>

<script>
import CButton from "@/components/CButton.vue";
import CSwitch from "@/components/CSwitch.vue";
import { onMounted, ref, defineComponent } from "vue";

export default defineComponent({
  name: "CCalculator",
  components: { CSwitch, CButton },
  setup() {
    const operations = ["+", "-", "*", "/", "%", "()"];
    const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "."];
    const currentNum = ref("");
    const prevNum = ref("");
    const selectedOperation = ref("");
    const total = ref("");
    const pressed = (value) => {
      if (value === "=" || value === "Enter") {
        historyData.push({
          operations: `${prevNum.value} ${selectedOperation.value} ${currentNum.value}`,
          sum: eval(`${prevNum.value}
          ${selectedOperation.value}
          ${currentNum.value}`),
        });
        calculate();
      } else if (value === "%") percentage();
      else if (value === "c") clear();
      else if (operations.includes(value)) applyOperation(value);
      else if (numbers.includes(value)) appendNumber(value);
    };
    const appendNumber = (value) => {
      currentNum.value = currentNum.value + value;
    };
    const applyOperation = (value) => {
      calculate();
      prevNum.value = currentNum.value;
      currentNum.value = "";
      selectedOperation.value = value;
    };
    const calculate = () => {
      if (selectedOperation.value === "*") multiply();
      if (selectedOperation.value === "()") multiply();
      else if (selectedOperation.value === "/") divide();
      else if (selectedOperation.value === "%") percentage();
      else if (selectedOperation.value === "-") subtract();
      else if (selectedOperation.value === "+") sum();
      prevNum.value = "";
      selectedOperation.value = "";
    };
    const multiply = () => {
      currentNum.value = prevNum.value * currentNum.value;
      total.value = currentNum.value;
    };
    const divide = () => {
      currentNum.value = prevNum.value / currentNum.value;
      total.value = currentNum.value;
    };
    const percentage = () => {
      currentNum.value = currentNum.value / 100;
      total.value = currentNum.value;
    };
    const subtract = () => {
      currentNum.value = prevNum.value - currentNum.value;
      total.value = currentNum.value;
    };
    const sum = () => {
      currentNum.value = +prevNum.value + +currentNum.value;
      total.value = currentNum.value;
    };
    const clear = () => {
      currentNum.value = "";
      prevNum.value = "";
      selectedOperation.value = "";
      currentNum.value = "";
    };
    const deleteValue = () => {
      if (currentNum.value.length !== 0 && currentNum.value !== "0") {
        currentNum.value = currentNum.value.slice(0, -1);
      }
    };
    const negateValue = () => {
      if (currentNum.value === "0") {
        return (currentNum.value = "-0");
      }
      if (currentNum.value === "-") {
        return (currentNum.value = "0");
      }
      if (currentNum.value === "0.") {
        return (currentNum.value = `-${currentNum.value}`);
      }
      if (currentNum.value === "-0.") {
        return (currentNum.value = "0.");
      }
      currentNum.value = `${currentNum.value * -1}`;
    };
    let historyData = [];

    const handleKeydown = (e) => {
      pressed(e.key);
    };
    onMounted(() => window.addEventListener("keydown", handleKeydown));

    return {
      currentNum,
      pressed,
      selectedOperation,
      prevNum,
      negateValue,
      deleteValue,
      total,
      historyData,
    };
  },
});
</script>
