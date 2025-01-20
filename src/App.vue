<template :class="{ dark: isDarkMode }">
  <div id="app" :class="{ dark: isDarkMode }">
    <DarkModeProvider>
      <Header />
      <router-view />
    </DarkModeProvider>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import DarkModeProvider from "./components/DarkModeProvider.vue";
import { inject } from "vue";

const isDarkMode = inject("isDarkMode");

export default {
  name: "App",
  components: {
    Header,
    DarkModeProvider,
  },
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
}

.dark {
  background-color: #4a4e51 !important;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

:root {
  --background-color: #ffffff;
  --text-color: #000000;
}

@media (max-width: 800px) {
  #app {
    display: flex;
    flex-direction: column-reverse;
  }
}

html,
body {
  margin: 0;
  padding: 0;
  overflow-x: hidden;
  width: 100%;
  height: 100%;
}

body {
  margin: 0px;
  background-color: #f6f6f6;
}
</style>
