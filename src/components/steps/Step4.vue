<template>
  <div>
    <Title
      title="Finishing Up"
      subtitle="Double-check everything looks OK before confirming"
    />

    <div class="bg-blue-50 rounded-lg shadow-none p-4 mx-auto mt-6">
      <div class="flex justify-between items-center mb-4">
        <div>
          <div class="text-gray-800 font-medium">Arcade (Monthly)</div>
          <button class="text-blue-500 text-sm mt-1">Change</button>
        </div>
        <div class="text-gray-800 font-medium">$9/mo</div>
      </div>

      <div class="border-t border-gray-200 mt-2 pt-2">
        <div class="flex justify-between items-center my-2">
          <div class="text-gray-600">Online service</div>
          <div class="text-gray-800">+ $1/mo</div>
        </div>
        <div class="flex justify-between items-center my-2">
          <div class="text-gray-600">Larger storage</div>
          <div class="text-gray-800">+ $2/mo</div>
        </div>
      </div>
    </div>
    <div class="p-4">
      <div class="border-t border-gray-200 mt-4 pt-2">
        <div class="flex justify-between items-center font-medium text-gray-800">
          <div>Total (per month)</div>
          <div class="text-blue-500">+ ${{ total }}/mo</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import type { PropType } from 'vue'
import Title from '../Title.vue';

const total = computed(() => {
  return 12
})
</script>
