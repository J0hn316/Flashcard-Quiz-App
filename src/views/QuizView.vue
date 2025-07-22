<template>
  <div class="max-w-xl mx-auto text-center mt-10">
    <div v-if="!quizCompleted">
      <Flashcard :card="currentCard" />

      <div class="mt-6 flex justify-center gap-4">
        <button
          class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded"
          @click="markAnswer(true)"
        >
          ✅ Correct
        </button>
        <button
          class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded"
          @click="markAnswer(false)"
        >
          ❌ Incorrect
        </button>
      </div>
    </div>

    <div v-else class="p-6 bg-white shadow-md rounded text-gray-700 mt-6">
      <h2 class="text-2xl font-bold mb-2">🎉 Quiz Complete!</h2>
      <p>You got {{ correctCount }} out of {{ flashcards.length }} correct.</p>
      <p class="mt-2 text-xl font-semibold">Score: {{ scorePercentage }}%</p>
      <button
        class="mt-4 bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded"
        @click="restartQuiz"
      >
        🔁 Restart Quiz
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import Flashcard from '../components/Flashcard.vue';
import type { Flashcard as FlashcardType } from '../types/Flashcard';

const flashcards: FlashcardType[] = [
  { id: 1, question: 'What is the capital of France?', answer: 'Paris' },
  { id: 2, question: 'What is 2 + 2?', answer: '4' },
  { id: 3, question: 'What is the largest ocean?', answer: 'Pacific Ocean' },
  { id: 4, question: 'Who wrote Hamlet?', answer: 'William Shakespeare' },
];

const currentIndex = ref(0);
const correctCount = ref(0);
const quizCompleted = ref(false);

const currentCard = computed(() => flashcards[currentIndex.value]);
const scorePercentage = computed(() =>
  Math.round((correctCount.value / flashcards.length) * 100)
);

const markAnswer = (isCorrect: boolean) => {
  if (isCorrect) correctCount.value++;

  if (currentIndex.value < flashcards.length - 1) {
    currentIndex.value++;
  } else {
    quizCompleted.value = true;
  }
};

const restartQuiz = () => {
  currentIndex.value = 0;
  correctCount.value = 0;
  quizCompleted.value = false;
};
</script>
