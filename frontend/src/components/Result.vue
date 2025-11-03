<script setup>
import { ref, onMounted } from 'vue'

const props = defineProps({
    typingResult: {
        type: Object,
        required: true,
    },
})
const emit = defineEmits(['resetTypingResult'])

const resultDiv = ref(null)
onMounted(() => {
    // Focus the div to capture keyboard events
    resultDiv.value?.focus()
})
</script>
<template>
    <div @keydown.tab="emit('resetTypingResult')" tabindex="0" ref="resultDiv" style="outline: none;">
        <h2>Test Completed!</h2>
        <p>Your Results:</p>
        <ul>
            <li>Start at {{ props.typingResult.startTime }} to {{ props.typingResult.endTime }}</li>
            <li>WPM: {{ props.typingResult.wpm }}</li>
            <li>Accuracy: {{ props.typingResult.accuracy }}%</li>
            <li>Correct Characters: {{ props.typingResult.correctChars }}</li>
            <li>Incorrect Characters: {{ props.typingResult.incorrectChars }}</li>
            <li>Total Characters: {{ props.typingResult.totalChars }}</li>
        </ul>
        <button @click="emit('resetTypingResult')">Restart Test</button>
    </div>
</template>
