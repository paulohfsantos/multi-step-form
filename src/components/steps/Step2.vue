<template>
  <div>
    <Title
      title="Select yout plan"
      subtitle="You have the option of monthly or yearly billing"
    />

    <section class="plans mt-5">
      <div class="flex justify-center w-full">
        <div class="grid grid-cols-1 sm:grid-cols-1 md:grid-cols-3 gap-10">
          <div
            v-for="plan in plans"
            :key="plan.name"
            class="bg-gray-50 rounded-lg shadow-none p-6 flex flex-col items-start cursor-pointer"
            :class="isSelected(plan) ? 'border-2 border-blue-800' : ''"
            @click="emitSelectPlan(plan)"
          >
            <div :class="`p-2 rounded-full ${plan.bgColor}`">
              <q-icon :name="plan.icon" size="sm" color="white" />
            </div>
            <div class="mt-4 text-lg font-medium text-blue-900">
              {{ plan.name }}
            </div>
            <div class="text-gray-500">
              ${{ plan.price }}/{{ billing }}
            </div>
          </div>
        </div>
      </div>

      <div class="toggle-container w-full bg-gray-100 p-4 mt-4">
        <div class="flex justify-center items-center">
          <div class="font-medium" :class="billingPeriod === 'monthly' ? 'text-blue-900' : 'text-gray-400'">
            Monthly
          </div>
          <div>
            <q-toggle
              :model-value="billingPeriod === 'yearly'"
              @update:model-value="emitUpdateBillingPeriod"
              color="blue-900"
              keepColor
            />
          </div>
          <div class="font-medium" :class="billingPeriod === 'yearly' ? 'text-blue-900' : 'text-gray-400'">
            Yearly
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import type { PropType } from 'vue'
import Title from '../Title.vue';
import type { Plan } from '../../types'

const props = defineProps({
  plans: {
    type: Array as PropType<Plan[]>,
    required: true,
  },
  selectedPlans: {
    type: Array as PropType<Plan[]>,
    required: true,
  },
  billingPeriod: {
    type: String as PropType<'monthly' | 'yearly'>,
    required: true,
  },
})

const emit = defineEmits(['update:selectedPlans', 'update:billingPeriod'])

const billing = computed(() => props.billingPeriod === 'monthly' ? 'mo' : 'yr')

function isSelected(plan: Plan) {
  return props.selectedPlans.some(p => p.id === plan.id)
}

function emitSelectPlan(plan: Plan) {
  emit('update:selectedPlans', plan)
}

function emitUpdateBillingPeriod(isYearly: boolean) {
  const period = isYearly ? 'yearly' : 'monthly';
  emit('update:billingPeriod', period);
}
</script>
