<template>
  <div class="flex flex-col gap-8">
    <step
      description="Your Info"
      :step="1"
      :current-step="currentStep === 1"
      @selectStep="selectStep"
    />
    <step
      description="Select Plan"
      :step="2"
      :current-step="currentStep === 2"
      @selectStep="selectStep"
    />
    <step
      description="Add-ons"
      :step="3"
      :current-step="currentStep === 3"
      @selectStep="selectStep"
    />
    <step
      description="Summary"
      :step="4"
      :current-step="currentStep === 4"
      @selectStep="selectStep"
    />
  </div>
</template>

<script setup lang="ts">
import Step from './StepComponent.vue'
import { ref } from 'vue'

let currentStep = ref(1)

function selectStep(step: number) {
  currentStep.value = step
}
</script>
