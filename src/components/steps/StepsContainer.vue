<template>
  <div class="flex flex-col gap-8">
    <step
      description="Your Info"
      :step="1"
      :current-step="stepStore.currentStep === 1"
      @selectStep="selectStep"
    />
    <step
      description="Select Plan"
      :step="2"
      :current-step="stepStore.currentStep === 2"
      @selectStep="selectStep"
    />
    <step
      description="Add-ons"
      :step="3"
      :current-step="stepStore.currentStep === 3"
      @selectStep="selectStep"
    />
    <step
      description="Summary"
      :step="4"
      :current-step="stepStore.currentStep === 4"
      @selectStep="selectStep"
    />
    <step
      description="Confirmation"
      :step="5"
      :current-step="stepStore.currentStep === 5"
      @selectStep="selectStep"
    />
  </div>
</template>

<script setup lang="ts">
import Step from './StepComponent.vue'
import { useSteps } from '../../stores/steps'

const stepStore = useSteps()

function selectStep(step: number) {
  stepStore.setStep(step)
}
</script>
