<template>
  <div class="flex flex-nowrap rounded-md bg-white w-[900px] gap-8 p-4">
    <aside :style="{
      backgroundImage: 'url(' + AsideImage + ')',
      backgroundSize: 'cover'
    }" class="w-[430px] h-[600px] p-8">
      <steps-container />
    </aside>
    <div class="flex flex-col w-full p-10 justify-between">
      <div v-if="stepStore.currentStep === 1">
        <step1 :form="formOne" />
      </div>
      <div v-if="stepStore.currentStep === 2">
        step 2
      </div>
      <div v-if="stepStore.currentStep === 3">
        step 3
      </div>
      <div v-if="stepStore.currentStep === 4">
        step 4
      </div>

      <div class="flex justify-end w-full">
        <q-btn
          v-if="stepStore.currentStep !== 1"
          class="font-bold py-4 px-8 rounded-md mt-8"
          flat
          @click="prevStep"
        >
          Go Back
        </q-btn>

        <q-btn
          class="bg-blue-900 text-white font-bold py-4 px-8 rounded-md mt-8 justify-end self-end place-self-end justify-self-end"
          @click="nextStep"
          :disabled="stepStore.currentStep === 4"
        >
          {{ stepStore.currentStep === 4 ? 'Confirm' : 'Next Step' }}
        </q-btn>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import StepsContainer from './steps/StepsContainer.vue'
import Step1 from './steps/Step1.vue'
import AsideImage from '../assets/images/bg-sidebar-desktop.svg'
import { useSteps } from '../stores/steps'
import { ref } from 'vue'

const stepStore = useSteps();

const formOne = ref({
  name: '',
  email: '',
  phone: '',
})

function nextStep() {
  if (stepStore.currentStep === 4) {
    return
  }
  stepStore.setStep(stepStore.currentStep + 1)
}

function prevStep() {
  if (stepStore.currentStep === 1) {
    return
  }
  stepStore.setStep(stepStore.currentStep - 1)
}
</script>
