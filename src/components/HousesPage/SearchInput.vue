<template>
  <div
    class="search-container"
    :class="{ 'search-container-dark': isDarkMode }"
  >
    <img
      class="search"
      src="@/assets/icons/actions/search.png"
      alt="Search input"
    />
    <input
      type="text"
      :value="search"
      placeholder="Search for a house"
      @input="onInput"
    />
    <img
      v-if="search.length > 0"
      class="clear"
      src="@/assets/icons/actions/grey-clear-icon.png"
      alt="Clear search"
      @click="clearSearch"
    />
  </div>
</template>

<script setup>
import { ref, watch, inject } from "vue";

const isDarkMode = inject("isDarkMode");

const props = defineProps({
  search: String,
});

const emit = defineEmits(["update:search", "input"]);

const search = ref(props.search || "");

watch(
  () => props.search,
  (newSearch) => {
    search.value = newSearch;
  }
);

const onInput = (event) => {
  emit("update:search", event.target.value);
  emit("input", event.target.value);
};

const clearSearch = () => {
  search.value = "";
  emit("update:search", "");
  emit("input", "");
};
</script>

<style scoped>
@media (max-width: 880px) {
  .search-container {
    width: 100%;
    display: flex;
  }

  .search-container input {
    width: 100%;
    flex: 1;
  }
}

.search-container {
  position: relative;
  margin-top: 15px;
}

.search-container img {
  position: absolute;
  height: 18px;
  width: 18px;
  top: 50%;
  transform: translateY(-50%);
  background: #ffffff9c;
  padding: 2px;
  border-radius: 4px;
}

.search-container .search {
  left: 10px;
}

.search-container .clear {
  right: 10px;
  cursor: pointer;
}

.search-container input {
  width: 380px;
  font-size: 16px;
  padding: 10px 40px 10px 40px;
  border: 0;
  border-radius: 5px;
  background-color: #e8e8e8;
  color: #4a4b4c;
  font-size: 14px;
  font-family: "Montserrat";
  font-weight: 500;
}

.search-container-dark input {
  background-color: #4a4e51;
  color: white;
}

.search-container input::placeholder {
  color: #c3c3c3;
  font-size: 14px;
  font-family: "Open Sans";
  font-weight: 400;
}

.search-container input:focus {
  outline: none;
}

.search-container input[type="text"] {
  padding-left: 40px;
  padding-right: 40px;
}

.resulf-of-search {
  margin-right: auto;
}
</style>
