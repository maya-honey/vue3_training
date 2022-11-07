<template>
  <h1>Vue 3 入門</h1>
  <p>{{ message }}</p>
  <p v-text="message"></p>
</template>

<script setup>
  const message = 'Hello World';
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
