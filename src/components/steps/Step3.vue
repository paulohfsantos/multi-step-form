<template>
  <div>
    <Title
      title="Pick Add-ons"
      subtitle="Add-ons help enhance your gaming experience"
    />

    <section class="mt-4">
      <div class="flex flex-col max-w-md mx-auto">
        <div class="mb-4 rounded-lg">
          <div
            v-for="addon in addons"
            :key="addon.id"
            class="mb-3 rounded-lg flex items-center justify-between py-3 px-4 bg-blue-100 border border-purple-900"
          >
            <div class="flex items-center">
              <q-checkbox
                :model-value="addon.checked"
                color="primary"
                @update:model-value="$event => updateSelected(addon.id, $event)"
              />
              <div>
                <p class="font-semibold">{{ addon.title }}</p>
                <p class="text-gray-400 text-xs">{{ addon.subtitle }}</p>
              </div>
            </div>
            <div class="text-purple-900">
              + ${{ addon.price }}/mo
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import type { PropType } from 'vue'
import Title from '../Title.vue';
import { AddOn } from 'src/types';

defineProps({
  onlineService: {
    type: Boolean,
    required: true,
  },
  addons: {
    type: Array as PropType<AddOn[]>,
    required: true,
  },
})

const emit = defineEmits(['update:selectedServices'])

const updateSelected = (id: number, selected: boolean) => {
  emit('update:selectedServices', { id, selected })
}

</script>
