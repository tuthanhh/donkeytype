<script setup>
import { RouterView } from 'vue-router'
import Header from './components/Header.vue'
</script>

<template>
  <div class="main-layout">
    <Header class="header" />
    <RouterView class="content" />
  </div>
</template>

<style scoped>
html,
body {
  height: 100vh;
  margin: 0;
  padding: 0;
  overflow: hidden;
}
.main-layout {
  display: flex;
  flex-direction: column;
  height: 100vh;
  min-height: 100vh;
  overflow: hidden;
}
.header {
  flex-shrink: 0;
}
.content {
  flex: 1;
  overflow: auto;
  min-height: 0;
  display: flex;
  flex-direction: column;
}
</style>
