<script setup>
import { ref, onMounted, computed, nextTick } from 'vue'
// Define props to accept numberOfWords
const emit = defineEmits(['update:result'])
const props = defineProps({
  numberOfWords: {
    type: Number,
    default: 50,
  },
  result: {
    type: Object,
    default: () => ({
      correctChars: 0,
      incorrectChars: 0,
      totalChars: 0,
      accuracy: 0,
      wpm: 0,
      startTime: null,
      endTime: null,
    }),
  },
})

// State variables
const typingText = ref('')
const loading = ref(true)

const input = ref('')
const inputRef = ref(null)
const currentIndex = computed(() => input.value.length)
const startTimeRef = ref(null)
const hasStarted = ref(false)

// Emit event when typing test is finished

function startTest() {
  hasStarted.value = true
  startTimeRef.value = Date.now() // Set the local start time
  const newResult = {
    ...props.result,
    startTime: startTimeRef.value, // Update the result with the local start time
    endTime: null,
  }
  emit('update:result', newResult)
}

function resetTest() {
  startTimeRef.value = null
  hasStarted.value = false
  const newResult = {
    ...props.result,
    startTime: null,
    endTime: null,
    correctChars: 0,
    incorrectChars: 0,
    totalChars: 0,
    accuracy: 0,
    wpm: 0,
  }
  emit('update:result', newResult)
}

function endTest() {
  hasStarted.value = false
  const correct = input.value.split('').filter((c, i) => c === typingText.value[i]).length
  const total = input.value.length
  const endTime = Date.now()
  const newResult = {
    ...props.result,
    correctChars: correct,
    incorrectChars: total - correct,
    totalChars: total,
    startTime: startTimeRef.value,
    endTime: endTime,
    wpm: Math.round(correct / 5 / ((endTime - startTimeRef.value) / 1000 / 60)), // Use startTimeRef here
    accuracy: Math.round((correct / total) * 100),
  }
  emit('update:result', newResult)
}

function updateStats() {
  let correct = 0
  let incorrect = 0
  for (let i = 0; i < input.value.length; i++) {
    if (input.value[i] === typingText.value[i]) correct++
    else incorrect++
  }
  const newResult = {
    ...props.result,
    startTime: startTimeRef.value,
    correctChars: correct,
    incorrectChars: incorrect,
    totalChars: input.value.length,
  }

  emit('update:result', newResult)
}

async function fetchWords() {
  loading.value = true
  typingText.value = ''
  input.value = ''

  // TODO: Fetch words from our API based on props.numberOfWords
  const response = await fetch(
    'https://random-word-api.herokuapp.com/word?number=' + props.numberOfWords,
  )

  const data = await response.json()
  typingText.value = data.join(' ')
  loading.value = false
  await nextTick()
  inputRef.value && inputRef.value.focus()
}

function onInput(e) {
  input.value = e.target.value

  if (input.value.length > 0 && !hasStarted.value) {
    startTest()
  }

  if (input.value.length >= typingText.value.length) {
    endTest()
  } else {
    updateStats()
  }
}

function onKeyDown(event) {
  if (event.key === 'Tab') {
    event.preventDefault()
    resetTest()
    fetchWords()
  }
}

onMounted(() => {
  fetchWords()
})
</script>

<template>
  <div class="game" @click="inputRef && inputRef.focus()">
    <div>{{ input.length + '/' + typingText.length }}</div>
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
