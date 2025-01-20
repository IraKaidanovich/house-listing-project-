<template>
  <header class="header" :class="{ 'dark-header': isDarkMode }">
    <div class="header-content">
      <nav class="navbar">
        <router-link
          :to="{ name: 'HousesPage' }"
          :class="[
            'nav-link',
            { active: isHomeActive, 'dark-link': isDarkMode },
          ]"
        >
          <span>Houses</span>
          <img
            v-if="isHomeActive"
            @click="goToHousesPage"
            class="image"
            :class="{ active: isHomeActive }"
            src="@/assets/icons/mobile/home-active-icon.png"
            alt="Houses page"
          />
          <img
            v-else
            @click="goToHousesPage"
            class="image"
            src="@/assets/icons/mobile/home-icon.png"
            alt="Houses page"
          />
        </router-link>
        <router-link
          :to="{ name: 'AboutPage' }"
          :class="[
            'nav-link',
            { active: isAboutActive, 'dark-link': isDarkMode },
          ]"
        >
          <span>About</span>
          <img
            v-if="isAboutActive"
            @click="goToAboutPage"
            class="image"
            :class="{ active: isAboutActive }"
            src="@/assets/icons/mobile/info-active-icon.png"
            alt="About page"
          />
          <img
            v-else
            @click="goToAboutPage"
            class="image"
            src="@/assets/icons/mobile/info-icon.png"
            alt="About page"
          />
        </router-link>
      </nav>
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
    </div>
  </header>
</template>

<script setup>
import { computed, inject } from "vue";
import { useRoute, useRouter } from "vue-router";

const router = useRouter();
const route = useRoute();

const isDarkMode = inject("isDarkMode");
const toggleDarkMode = inject("toggleDarkMode");

if (!isDarkMode || !toggleDarkMode) {
  console.error(
    "Dark mode state or toggle function is missing. Ensure the parent provides these."
  );
}

const goToHousesPage = () => {
  router.push({ name: "HousesPage" });
};

const goToAboutPage = () => {
  router.push({ name: "AboutPage" });
};

const isHomeActive = computed(() => {
  return [
    "HousesPage",
    "HouseCreatingPage",
    "HouseDetailsPage",
    "HouseEditPage",
  ].includes(route.name);
});

const isAboutActive = computed(() => route.name === "AboutPage");
</script>

<style scoped>
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

.navbar {
  width: 100%;
  display: flex;
  justify-content: flex-start;
}

@media (min-width: 880px) {
  img.image {
    display: none;
  }
}

@media (max-width: 880px) {
  .dark-mode {
    display: none;
  }

  .nav-link:last-of-type {
    margin-inline-start: auto;
  }

  .nav-link span {
    display: none;
  }

  .nav-link img {
    width: 30px;
    height: 30px;
    position: relative;
    transition: transform 0.2s ease, color 0.2s ease;
  }

  .nav-link img.active {
    width: 30px;
    height: 30px;
    transform: scale(1.1);
  }

  .header {
    position: fixed;
    bottom: 0px;
    z-index: 1;
    width: 100%;
    height: 50px;
    box-shadow: 0px 1px 20px 0px rgba(62, 63, 63, 0.226);
  }
}

.header {
  display: flex;
  align-items: center;
  padding: 0px;
  background-color: #fff;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.dark-header {
  background-color: #4a4e51;
}

.nav-link {
  text-decoration: none;
  color: inherit;
  font-size: 18px;
  font-family: "Montserrat";
  color: #c3c3c3;
  font-weight: 500;
  margin: 0px 40px 0px 0px;
}

.router-link-active,
.active {
  font-weight: bold;
  color: black;
  transition: font-weight 0.2s ease, color 0.2s ease;
}

.dark-link {
  color: #fff;
}

.header-content {
  display: flex;
  padding: 0% 15%;
  align-items: center;
  width: 100%;
  height: 60px;
}
</style>
