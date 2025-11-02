<script setup>
import { useRouter } from 'vue-router'

const router = useRouter()

function goHome() {
  router.replace({ name: 'home' })
}
</script>

<template>
  <div class="header-container">
    <div @click="goHome" class="left-header">
      <img src="../assets/logo.svg" alt="DonkeyType Logo" width="50" />
      <h1 @click="">DonkeyType</h1>
    </div>
  </div>
</template>

<style scoped>
.header-container {
  border-bottom: 1px solid #ddd;
  display: flex;
  justify-content: left;
}
.left-header {
  display: flex;
  align-items: left;
  gap: 20px;
  padding: 0px 0px 20px 80px;
  cursor: pointer;
}
</style>
