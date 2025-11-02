<script setup>
import TypingArea from '../components/TypingArea.vue'
</script>
<template>
  <div class="home-view">
    <div class="typing-area">
      <TypingArea />
    </div>
    <div class="info-text">
      <p>Click anywhere to focus. Press Tab to get new words.</p>
    </div>
  </div>
</template>
<style scoped>
.home-view {
  display: flexbox;
  flex-direction: column;
}
.typing-area {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  flex: 1 1 0%;
  min-height: 0;
  overflow: auto;
}
.info-text {
  text-align: center;
  margin-top: 20px;
  color: var(--color-foreground);
  flex: 0 0 auto;
}
</style>
