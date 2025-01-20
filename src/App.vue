<template>
  <div id="app">
    <DarkModeProvider>
      <Header />
      <router-view />
    </DarkModeProvider>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import DarkModeProvider from "./components/DarkModeProvider.vue";

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

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100%;
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
