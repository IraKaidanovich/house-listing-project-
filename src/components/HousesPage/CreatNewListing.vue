<template>
  <button
    @click="goToHouseCreating"
    class="creat-new"
    :class="{ 'create-new-dark': isDarkMode }"
  >
    + CREAT NEW
  </button>
</template>

<script setup>
import { useRouter } from "vue-router";
import { inject } from "vue";

const isDarkMode = inject("isDarkMode");

const router = useRouter();

// Define the method to navigate to the House Creating page
const goToHouseCreating = () => {
  router
    .push({ name: "HouseCreatingPage" })
    .then(() => {})
    .catch((error) => {});
};
</script>

<style scoped>
@media (min-width: 880px) {
  img.plus {
    display: none;
  }
}

@media (max-width: 880px) {
  .creat-new {
    display: none;
  }
}

.creat-new {
  background-color: #eb5440;
  color: #ffffff;
  padding: 8px 25px;
  border-radius: 5px;
  border: none;
  font-size: 18px;
  font-family: "Montserrat";
  font-weight: 600;
  margin: 30px 0px;
  cursor: pointer;
}

.create-new-dark {
  background-color: #9c33258a;
}
</style>
