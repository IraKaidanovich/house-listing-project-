<template>
  <div id="app">
    <DarkModeProvider>
      <Header />
    </DarkModeProvider>
    <router-view />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import DarkModeProvider from "./components/DarkModeProvider.vue";

export default {
  name: "App",
  components: {
    Header,
  },
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
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

body.dark-mode {
  --background-color: #121212;
  --text-color: #ffffff;
}

body {
  background-color: var(--background-color);
  color: var(--text-color);
  transition: background-color 0.3s ease, color 0.3s ease;
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
}

body {
  margin: 0px;
  background-color: #f6f6f6;
}
</style>
