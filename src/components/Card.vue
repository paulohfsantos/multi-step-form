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
        <step2
          :plans="plans"
          :selectedPlans="selectedPlans"
          :billingPeriod="billingPeriod"
          @update:selectedPlans="selectPlan"
          @update:billingPeriod="updateBillingPeriod"
        />
      </div>
      <div v-if="stepStore.currentStep === 3">
        <step3
          :addons="addons"
          :onlineService="serviceSelected"
          @update:selectedServices="updateServices"
        />
      </div>
      <div v-if="stepStore.currentStep === 4">
        <step4
          :addonChoosen="addons"
          :plansChoosen="selectedPlans"
          :billingPeriod="billingPeriod"
          @goToStep="goToStep"
        />
      </div>

      <div class="flex w-full" :class="isFirstStep ? 'justify-between' : 'justify-end'">
        <q-btn
          v-if="isFirstStep"
          class="font-bold py-4 px-8 rounded-md mt-8 text-blue-900"
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
import Step2 from './steps/Step2.vue'
import Step3 from './steps/Step3.vue'
import Step4 from './steps/Step4.vue'
import AsideImage from '../assets/images/bg-sidebar-desktop.svg'

import { useSteps } from '../stores/steps'
import { ref, computed } from 'vue'
import type { Plan, AddOn } from '../types'

const stepStore = useSteps();

const formOne = ref({
  name: '',
  email: '',
  phone: '',
})

const plans = ref<Plan[]>([
  {
    id: 1,
    name: 'Arcade',
    price: '9',
    icon: 'games',
    bgColor: 'bg-orange-300',
  },
  {
    id: 2,
    name: 'Advanced',
    price: '12',
    icon: 'videogame_asset',
    bgColor: 'bg-red-300',
  },
  {
    id: 3,
    name: 'Pro',
    price: '15',
    icon: 'sports_esports',
    bgColor: 'bg-blue-300',
  },
])

const addons = ref<AddOn[]>([
  {
    id: 1,
    title: 'Online Service',
    subtitle: 'Access to multiplayer games',
    checked: false,
    price: 1,
  },
  {
    id: 2,
    title: 'Larger storage',
    subtitle: 'Extra 1GB of cloud save',
    checked: false,
    price: 2,
  },
])

const isFirstStep = computed(() => stepStore.currentStep !== 1)

const selectedPlans = ref<Plan[]>([])
const billingPeriod = ref<'monthly' | 'yearly'>('monthly')
const serviceSelected = ref(false)

function goToStep(step: number) {
  stepStore.setStep(step)
}

function selectPlan(plan: Plan) {
  if (selectedPlans.value.includes(plan)) {
    selectedPlans.value = selectedPlans.value.filter((p) => p.id !== plan.id)
  } else {
    selectedPlans.value = [...selectedPlans.value, plan]
  }
}

function updateServices(info: { id: number; selected: boolean }) {
  const index = addons.value.findIndex(a => a.id === info.id);
  if (index !== -1) {
    addons.value[index] = { ...addons.value[index], checked: info.selected };
  }
}

function updateBillingPeriod(period: 'monthly' | 'yearly') {
  billingPeriod.value = period
}

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
