<template>
  <div>
    <h1 class="text-3xl font-bold">Personal Info</h1>
    <p class="text-gray-500">Please provide your name, email address, and phone number.</p>

    <q-form class="q-gutter-md mt-4">
      <div class="input-control">
        <label class="text-blue-900 font-medium" for="name">Name</label>
        <q-input outlined placeholder="Name" v-model="form.name" />
      </div>
      <div class="input-control">
        <label class="text-blue-900 font-medium" for="name">Email</label>
        <q-input outlined placeholder="Email" v-model="form.email" type="email" />
      </div>
      <div class="input-control">
        <label class="text-blue-900 font-medium" for="name">Phone</label>
        <q-input outlined placeholder="Phone" v-model="form.phone" mask="(##) # ####-####" />
      </div>
    </q-form>
  </div>
</template>

<script setup lang="ts">
import type { PropType } from 'vue'

type Form = {
  name: string
  email: string
  phone: string
}

defineProps({
  form: {
    type: Object as PropType<Form>,
    required: true,
  },
})
</script>
