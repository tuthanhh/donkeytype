<script setup>
const props = defineProps({
  typingResult: {
    type: Object,
    required: true,
  },
})
const emit = defineEmits(['resetTypingResult'])
</script>
<template>
  <h2>Test Completed!</h2>
  <p>Your Results:</p>
  <ul>
    <li>Start at {{ typingResult.startTime }} to {{ typingResult.endTime }}</li>
    <li>WPM: {{ typingResult.wpm }}</li>
    <li>Accuracy: {{ typingResult.accuracy }}%</li>
    <li>Correct Characters: {{ typingResult.correctChars }}</li>
    <li>Incorrect Characters: {{ typingResult.incorrectChars }}</li>
    <li>Total Characters: {{ typingResult.totalChars }}</li>
  </ul>
  <button @click="emit('resetTypingResult')">Restart Test</button>
</template>
