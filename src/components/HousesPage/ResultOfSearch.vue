<template>
  <div v-if="hasSearched" class="result-container">
    <div class="resulf-of-search">
      <h4 v-if="filteredItems.length > 0" :class="{ dark: isDarkMode }">
        {{ filteredItems.length }} {{ resultLabel }} found
      </h4>
    </div>
    <div v-if="filteredItems.length === 0" class="no-results">
      <img src="@/assets/images/no-houses-found.png" alt="No results found" />
      <p class="no-results-text" :class="{ dark: isDarkMode }">
        No results found
      </p>
      <p class="no-results-text" :class="{ dark: isDarkMode }">
        Please try another keyword
      </p>
    </div>
  </div>
</template>

<script setup>
import { computed, inject } from "vue";
import { defineProps } from "vue";

const isDarkMode = inject("isDarkMode");

// Define the props
const props = defineProps({
  filteredItems: Array,
  search: String,
  hasSearched: Boolean,
});

// Result label computed property
const resultLabel = computed(() => {
  return props.filteredItems.length === 1 ? "result" : "results";
});
</script>

<style scoped>
.dark {
  color: white !important;
}

.resulf-of-search {
  margin-right: auto;
}

.no-results img {
  width: 450px;
  height: auto;
  margin-bottom: 20px;
}

.no-results {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 100px 0px;
}
</style>
