<template>
  <div class="flex gap-4">
    <div :class="currentStep ? 'current step' : 'step'">
      {{ step }}
    </div>
    <div class="flex flex-col">
      <p class="text-blue-200">STEP {{ step }}</p>
      <p class="uppercase font-bold text-white">{{ description }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps({
  step: {
    type: Number,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
  currentStep: {
    type: Boolean,
    required: true,
  },
});
</script>

<style lang="postcss">
.step {
  @apply text-white rounded-full w-10 h-10 flex items-center justify-center border;
}

.current {
  @apply bg-[#bfe2fd] text-black;
}
</style>
