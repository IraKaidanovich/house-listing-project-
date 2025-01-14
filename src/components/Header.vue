<template>
  <header class="header">
    <div class="header-content">
      <!-- Logo -->
      <div @click="goToHousesPage" class="logo">
        <img src="@/assets/images/logo.png" alt="Logo of DTT company" />
      </div>

      <!-- Navigation Bar -->
      <nav class="navbar">
        <router-link
          :to="{ name: 'HousesPage' }"
          class="nav-link"
          exact-active-class="active"
        >
          <span>Houses</span>
          <img
            class="image"
            :src="isHomeActive ? homeActiveIcon : homeIcon"
            alt="Houses page"
          />
        </router-link>
        <router-link
          :to="{ name: 'AboutPage' }"
          class="nav-link"
          exact-active-class="active"
        >
          <span>About</span>
          <img
            class="image"
            :src="isAboutActive ? aboutActiveIcon : aboutIcon"
            alt="About page"
          />
        </router-link>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { computed } from "vue";
import { useRoute, useRouter } from "vue-router";

// Router instance
const router = useRouter();
const route = useRoute();

// Navigation methods
const goToHousesPage = () => {
  router.push({ name: "HousesPage" });
};

// Active state for navigation links
const isHomeActive = computed(() => {
  return [
    "HousesPage",
    "HouseCreatingPage",
    "HouseDetailsPage",
    "HouseEditPage",
  ].includes(route.name);
});

const isAboutActive = computed(() => route.name === "AboutPage");

// Dynamic imports for icons
const homeIcon = require("@/assets/icons/mobile/home-icon.png");
const homeActiveIcon = require("@/assets/icons/mobile/home-active-icon.png");
const aboutIcon = require("@/assets/icons/mobile/info-icon.png");
const aboutActiveIcon = require("@/assets/icons/mobile/info-active-icon.png");
</script>

<style scoped>
/* Navbar styles */
.navbar {
  width: 100%;
  display: flex;
  justify-content: flex-start;
}

/* Responsive design */
@media (min-width: 880px) {
  img.image {
    display: none;
  }
}

@media (max-width: 880px) {
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
    top: 7px;
  }
}

/* Header styles */
.header {
  position: fixed;
  bottom: 0px;
  z-index: 1;
  width: 100%;
  height: 50px;
  box-shadow: 0px 1px 20px 0px rgba(62, 63, 63, 0.226);
  background-color: #fff;
  display: flex;
  align-items: center;
}

.logo img {
  height: 30px;
}

.logo {
  margin-left: 0px;
  cursor: pointer;
  display: flex;
  align-items: center;
}

/* Link styles */
.nav-link {
  text-decoration: none;
  color: #c3c3c3;
  font-size: 18px;
  font-family: "Montserrat";
  font-weight: 500;
  margin: 0px 20px;
}

.router-link-active,
.active {
  font-weight: bold;
  color: black;
}

.header-content {
  display: flex;
  padding: 0 15%;
  align-items: center;
  width: 100%;
}
</style>
