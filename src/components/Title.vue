<template>
  <h1 class="text-3xl font-bold text-blue-950">{{ title }}</h1>

  <p class="text-gray-500">
    {{ subtitle }}
  </p>
</template>

<script setup lang="ts">
defineProps({
  title: {
    type: String,
    required: true,
  },
  subtitle: {
    type: String,
    required: true,
  },
})
</script>
