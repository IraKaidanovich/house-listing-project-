<template>
  <div class="filter">
    <button
      class="price-filter"
      :class="{
        active: sortCriteria === 'price',
        dark: isDarkMode && sortCriteria === 'price',
      }"
      @click="$emit('toggle', 'price')"
    >
      Price
    </button>
    <button
      class="size-filter"
      :class="{
        active: sortCriteria === 'size',
        dark: isDarkMode && sortCriteria === 'size',
      }"
      @click="$emit('toggle', 'size')"
    >
      Size
    </button>
  </div>
</template>

<script setup>
import { toRefs, inject } from "vue";

const isDarkMode = inject("isDarkMode");

const props = defineProps({
  sortCriteria: String,
});

const { sortCriteria } = toRefs(props);
</script>

<style scoped>
@media (max-width: 880px) {
  .filter {
    display: flex;
    margin-top: 15px;
    width: 100%;
    justify-content: space-between;
  }

  .filter button {
    flex: 1;
  }
}

.price-filter,
.size-filter {
  color: #ffffff;
  padding: 8px 40px;
  border: none;
  font-size: 14px;
  font-family: "Montserrat";
  font-weight: 600;
  cursor: pointer;
  background-color: #c3c3c3;
  transition: background-color 0.4s ease;
}

.price-filter {
  border-radius: 5px 0px 0px 5px;
}

.size-filter {
  border-radius: 0px 5px 5px 0px;
}

.active {
  background-color: #eb5440;
}

.dark {
  background-color: #9c33258a;
}
</style>
