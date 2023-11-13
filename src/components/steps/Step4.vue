<template>
  <div>
    <Title
      title="Finishing Up"
      subtitle="Double-check everything looks OK before confirming"
    />

    <div class="bg-blue-50 rounded-lg shadow-none p-4 mx-auto mt-6">
      <div v-for="plan in plansChoosen" class="flex justify-between items-center mb-4">
        <div>
          <div class="text-blue-950 font-semibold">
            {{ plan.name }} ({{ billingPeriod }})
          </div>
        </div>
        <div class="text-blue-950 font-semibold">
          ${{ plan.price }} / {{ billing }}
        </div>
      </div>
      <div>
        <button @click="goToStep" class="text-gray-500 underline text-sm mt-1">
          Change
        </button>
      </div>

      <div class="border-t border-gray-200 mt-2 pt-2">
        <div v-for="addon in addonChoosen" class="flex justify-between items-center my-2">
          <div class="text-gray-500">{{ addon.title }}</div>
          <div class="text-gray-500">
            + ${{ addon.price }}/ {{ billing }}
          </div>
        </div>
      </div>
    </div>
    <div class="p-4">
      <div class="border-t border-gray-200 mt-4 pt-2">
        <div class="flex justify-between items-center font-medium text-gray-800">
          <div>Total ({{ perPeriod }})</div>
          <div class="text-blue-800 text-lg">${{ total }}/mo</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { PropType } from 'vue'
import { computed } from 'vue'
import { AddOn, Plan } from 'src/types';
import Title from '../Title.vue';

const props = defineProps({
  plansChoosen: {
    type: Array as PropType<Plan[]>,
    required: true,
  },
  billingPeriod: {
    type: String as PropType<'monthly' | 'yearly'>,
    required: true,
  },
  addonChoosen: {
    type: Array as PropType<AddOn[]>,
    required: true,
  },
})

const emit = defineEmits(['goToStep'])

const billing = computed(() => {
  return props.billingPeriod === 'monthly' ? 'mo' : 'yr'
})

const perPeriod = computed(() => {
  return props.billingPeriod === 'monthly' ? 'per month' : 'per year'
})

const total = computed(() => {
  const plansTotal = props.plansChoosen.reduce((acc, plan) => {
    return acc + Number(plan.price)
  }, 0)

  const addonsTotal = props.addonChoosen.reduce((acc, addon) => {
    return acc + Number(addon.price)
  }, 0)

  return plansTotal + addonsTotal
})

const goToStep = () => {
  emit('goToStep', 2)
}
</script>
