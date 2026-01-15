<script setup lang="ts">
import Countdown from "./components/countdown.vue";
</script>

<template>
  <Countdown />
</template>

<style>
/* Base styles for mobile-first approach */
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  font-family: 'Noto Sans KR', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width: 100%;
  min-height: 100vh;
  margin: 0;
  padding: 0;
}

/* Add Instrument Serif font */
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&display=swap');
</style>
