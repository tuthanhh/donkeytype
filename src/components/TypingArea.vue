<script setup>
import { ref, onMounted, computed, nextTick } from 'vue'
const typingText = ref('')
const loading = ref(true)
const numberOfWords = ref(30)
const input = ref('')
const inputRef = ref(null)
const currentIndex = computed(() => input.value.length)

async function fetchWords() {
  loading.value = true
  typingText.value = ''
  input.value = ''
  const response = await fetch(
    'https://random-word-api.herokuapp.com/word?number=' + numberOfWords.value,
  )

  const data = await response.json()
  typingText.value = data.join(' ')
  loading.value = false
  await nextTick()
  inputRef.value && inputRef.value.focus()
}

function onInput(e) {
  const val = e.target.value
  // Only allow up to the length of typingText
  if (val.length > typingText.value.length) return
  input.value = val
  currentIndex.value = val.length
}

function onKeyDown(event) {
  if (event.key === 'Tab') {
    event.preventDefault()
    fetchWords()
  }
}

onMounted(() => {
  fetchWords()
})
</script>

<template>
  <div class="game" @click="inputRef && inputRef.focus()">
    <div v-if="loading">Loading words...</div>
    <div v-else class="word-list" tabindex="0">
      <input
        ref="inputRef"
        @input="onInput"
        @keydown="onKeyDown"
        autocorrect="off"
        autocomplete="off"
        spellcheck="false"
        class="hidden-input"
        v-model="input"
      />
      <span v-for="(char, index) in typingText" :key="index">
        <span
          :class="{
            correct: index < currentIndex && char === input[index],
            incorrect: index < currentIndex && char !== input[index],
            active: index === currentIndex,
            untyped: index >= currentIndex,
          }"
        >
          <template v-if="char === ' '">&nbsp;</template>
          <template v-else>{{ char }}</template>
        </span>
      </span>
    </div>
  </div>
</template>

<style>
.game {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  cursor: text;
}
.word-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  font-size: 1.5em;
  margin-bottom: 20px;
  outline: none;
}

.hidden-input {
  position: absolute;
  opacity: 0;
  pointer-events: none;
  z-index: -1;
}

.correct {
  color: --var(--color-background);
}
.incorrect {
  color: red;
  text-decoration: underline red 1.5px;
}
.untyped {
  opacity: 0.7;
}
.active {
  border-bottom: 2px solid #1976d2;
  background: #e3f2fd;
  animation: blink 1s steps(1) infinite;
}
@keyframes blink {
  0%,
  100% {
    background: #e3f2fd;
  }
  50% {
    background: transparent;
  }
}
</style>
