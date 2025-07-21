<template>
  <div
    class="w-full h-64 sm:h-72 perspective cursor-pointer"
    @click="toggleFlip"
  >
    <div
      class="relative w-full h-full transition-transform duration-500 transform-style-preserve-3d"
      :class="{ 'rotate-y-180': flipped }"
    >
      <!-- Front -->
      <div
        class="absolute inset-0 flex items-center justify-center text-xl bg-white text-gray-800 rounded shadow-md backface-hidden p-4"
      >
        {{ card.question }}
      </div>
      <!-- Back -->
      <div
        class="absolute inset-0 flex items-center justify-center text-xl bg-blue-600 text-white rounded shadow-md backface-hidden rotate-y-180 p-4"
      >
        {{ card.answer }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { Flashcard } from '../types/Flashcard';

defineProps<{ card: Flashcard }>();

const flipped = ref(false);

function toggleFlip() {
  flipped.value = !flipped.value;
}
</script>

<style scoped>
.perspective {
  perspective: 1000px;
}
.transform-style-preserve-3d {
  transform-style: preserve-3d;
}
.rotate-y-180 {
  transform: rotateY(180deg);
}
.backface-hidden {
  backface-visibility: hidden;
}
</style>
