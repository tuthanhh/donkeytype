<script setup>
import TypingArea from '../components/TypingArea.vue'
import Result from '../components/Result.vue'
import { ref } from 'vue'
const numberOfWords = ref(5)

// Result stats
const typingResult = ref({
  correctChars: 0,
  incorrectChars: 0,
  totalChars: 0,
  accuracy: 0,
  wpm: 0,
  startTime: null,
  endTime: null,
})
function resetTypingResult() {
  typingResult.value = {
    correctChars: 0,
    incorrectChars: 0,
    totalChars: 0,
    accuracy: 0,
    wpm: 0,
    startTime: null,
    endTime: null,
  }
}
</script>

<template>
  <div class="home-view">
    <div
      v-if="typingResult.endTime === null"
      style="display: flex; flex-direction: column; height: 100%"
    >
      <div class="typing-area">
        <TypingArea :number-of-words="numberOfWords" v-model:result="typingResult" />
      </div>
      <div class="info-text">
        <p>Click anywhere to focus. Press Tab to get new words.</p>
      </div>
    </div>

    <div v-else style="display: flex; flex-direction: column; height: 100%">
      <div class="typing-area">
        <Result :typing-result="typingResult" @resetTypingResult="resetTypingResult" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.home-view {
  display: flex; /* Corrected from flexbox to flex */
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
