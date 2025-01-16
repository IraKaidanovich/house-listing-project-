<template>
  <div>
    <slot />
  </div>
</template>

<script setup>
import { ref, provide } from 'vue';

// Global dark mode state
const isDarkMode = ref(false);

// Provide the state and a method to toggle it
provide('isDarkMode', isDarkMode);
provide('toggleDarkMode', () => {
  isDarkMode.value = !isDarkMode.value;
});
</script>
