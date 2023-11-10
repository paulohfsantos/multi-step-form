<template>
  <q-stepper v-model="step" animated class="q-stepper--tailwind">
    <q-step :name="1" title="Your Info" class="step-class">
      <div class="form-content mt-4">
        <input type="text" placeholder="Name" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-blue-500" />
        <input type="email" placeholder="Email Address" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-blue-500 mt-4" />
        <input type="tel" placeholder="Phone Number" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-blue-500 mt-4" />
      </div>
    </q-step>
    <!-- Add other q-steps here for steps 2, 3, and 4 -->
    <q-stepper-navigation>
      <q-btn flat label="Back" @click="previous" class="bg-gray-100 text-gray-800 hover:bg-gray-200 mr-2" :disable="step === 1" />
      <q-btn label="Next" @click="next" class="bg-blue-500 text-white hover:bg-blue-600" :disable="step === 4" />
    </q-stepper-navigation>
  </q-stepper>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const step = ref(1)

const next = () => {
  if (step.value < 3) {
    step.value++
  }
}

const previous = () => {
  if (step.value === 1) {
    return
  }

  if (step.value > 1) {
    step.value--
  }
}
</script>
