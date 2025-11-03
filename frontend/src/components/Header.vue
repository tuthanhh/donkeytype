<script setup>
import { useRouter, RouterLink } from 'vue-router'

const router = useRouter()

function goHome() {
  router.replace({ name: 'home' })
}
</script>

<template>
  <header class="header-container">
    <!-- Clickable logo + title to go home -->
    <div class="left-header" @click="goHome">
      <img src="../assets/logo.svg" alt="DonkeyType Logo" class="logo" />
      <h1 class="title">Donkeytype</h1>
    </div>

    <!-- Navigation link -->
    <RouterLink class="about-link" to="/about"> About the project </RouterLink>
  </header>
</template>

<style scoped>
.header-container {
  display: flex;
  justify-content: space-between; /* ensure spacing between left and right items */
  align-items: center;
  padding: 0 80px;
  height: 70px;
  border-bottom: 1px solid #ddd;
}

.left-header {
  display: flex;
  align-items: center;
  gap: 20px;
  cursor: pointer;
}

.logo {
  width: 50px;
  height: auto;
}

.title {
  margin: 0;
  font-size: 1.5rem;
}

.about-link {
  text-decoration: none;
  color: inherit;
  font-weight: 500;
}

.about-link:hover {
  text-decoration: underline;
}
</style>
