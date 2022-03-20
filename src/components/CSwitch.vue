<template>
  <div class="calculator-switch" @click="changeTheme">
    <span class="calculator-switch__titles">
      <span class="calculator-switch__title">Dark</span>
      <span class="calculator-switch__title">Light</span>
    </span>
    <input
      type="checkbox"
      class="calculator-switch__input"
      v-model="themeMode"
    />
    <span class="calculator-switch__toggle"></span>
  </div>
</template>

<script lang="ts">
import { onMounted, ref } from "vue";

enum ThemModeValue {
  Dark = "Dark",
  Light = "Light",
}

export default {
  name: "CSwitch",
  setup() {
    const themeMode = ref<boolean>(false);

    const changeTheme = () => {
      const html = document.getElementsByTagName("html")[0];

      themeMode.value = !themeMode.value;

      if (themeMode.value) {
        html.classList.add("light-mode");
        window.localStorage.setItem("theme-mode", ThemModeValue.Light);
      } else {
        html.classList.remove("light-mode");
        window.localStorage.setItem("theme-mode", ThemModeValue.Dark);
      }
    };

    onMounted(() => {
      const selectedMode = window.localStorage.getItem("theme-mode");

      if (selectedMode === ThemModeValue.Light) {
        themeMode.value = true;
      } else if (selectedMode === ThemModeValue.Dark) {
        themeMode.value = false;
      } else {
        window.localStorage.setItem("theme-mode", ThemModeValue.Dark);
        themeMode.value = false;
      }

      changeTheme();
    });

    return {
      themeMode,
      changeTheme,
    };
  },
};
</script>
