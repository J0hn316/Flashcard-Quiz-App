<template>
  <div class="min-h-screen bg-gray-200 p-6 flex justify-center items-center">
    <Flashcard :card="sampleCard" />
  </div>
</template>

<script setup lang="ts">
import Flashcard from './components/Flashcard.vue';
import type { Flashcard as FlashcardType } from './types/Flashcard';

const sampleCard: FlashcardType = {
  id: 1,
  question: 'What is the capital of France?',
  answer: 'Paris',
};
</script>
