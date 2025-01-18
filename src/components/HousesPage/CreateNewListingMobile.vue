<template>
  <div class="create-new-mobile">
    <button
      class="dark-mode"
      :class="{
        'light-mode-button': !isDarkMode,
        'dark-mode-button': isDarkMode,
      }"
      @click="toggleDarkMode"
      aria-label="Toggle dark mode"
      :aria-pressed="isDarkMode"
    >
      {{ isDarkMode ? "🌙" : "☀️" }}
    </button>
    <h1 class="title" :class="{ 'title-dark': isDarkMode }">Houses</h1>
    <img
      @click="goToHouseCreating"
      class="plus"
      src="@/assets/icons/actions/upload.png"
      alt="Create new button"
    />
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import { inject } from "vue";

const router = useRouter();

const isDarkMode = inject("isDarkMode");
const toggleDarkMode = inject("toggleDarkMode");

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
  .dark-mode {
    display: none;
  }
}

@media (max-width: 880px) {
  img.plus {
    width: 25px;
    height: 25px;
    margin-left: auto;
  }

  .title {
    font-size: 22px;
  }
}

.create-new-mobile {
  display: flex;
  flex-direction: row;
  align-items: center;
  width: 100%;
  gap: 30%;
}

.title-dark {
  color: white;
}

/* Light Mode Button */
.light-mode-button {
  padding: 12px 20px;
  border: none;
  border-radius: 25px;
  font-weight: bold;
  font-size: 1rem;
  cursor: pointer;
  background-color: #eb5440;
  color: #ffffff;
  box-shadow: 0 4px 8px rgba(235, 84, 64, 0.3);
  transition: background-color 0.3s ease, box-shadow 0.3s ease,
    transform 0.1s ease;
}

.light-mode-button:hover {
  background-color: #d94535;
  box-shadow: 0 6px 12px rgba(235, 84, 64, 0.5);
}

.light-mode-button:active {
  transform: scale(0.95);
}

/* Dark Mode Button */
.dark-mode-button {
  padding: 12px 20px;
  border: none;
  border-radius: 25px;
  font-weight: bold;
  font-size: 1rem;
  cursor: pointer;
  background-color: #616161;
  color: #ffffff;
  box-shadow: 0 4px 8px rgba(97, 97, 97, 0.3);
  transition: background-color 0.3s ease, box-shadow 0.3s ease,
    transform 0.1s ease;
}

.dark-mode-button:hover {
  background-color: #4a4a4a;
  box-shadow: 0 6px 12px rgba(97, 97, 97, 0.5);
}

.dark-mode-button:active {
  transform: scale(0.95);
}
</style>
