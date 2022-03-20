<template>
  <label class="calculator-switch">
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
  </label>
</template>

<script lang="ts">
import { computed, onMounted, ref } from "vue";

enum ThemModeValue {
  Dark = "Dark",
  Light = "Light",
}

export default {
  name: "CSwitch",
  setup() {
    const themeMode = ref<boolean>(false);

    // eslint-disable-next-line vue/return-in-computed-property
    const changeTheme = computed(() => {
      const html = document.getElementsByTagName("html")[0];

      if (themeMode.value) {
        html.classList.add("light-mode");
        window.localStorage.setItem("theme-mode", "Light");
      } else {
        html.classList.remove("light-mode");
        window.localStorage.setItem("theme-mode", ThemModeValue.Dark);
      }
    });

    onMounted(() => {
      const selectedMode = window.localStorage.getItem("theme-mode");
      if (selectedMode === ThemModeValue.Light) {
        themeMode.value = true;
      } else if (selectedMode === ThemModeValue.Dark) {
        themeMode.value = false;
      } else {
        window.localStorage.setItem("theme-mode", ThemModeValue.Dark);
      }
    });

    return {
      themeMode,
      changeTheme,
    };
  },
};
</script>
