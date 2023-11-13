<template>
  <div>
    <Title
      title="Personal Info"
      subtitle="Please provide your name, email address, and phone number."
    />

    <q-form class="q-gutter-md mt-4">
      <div class="input-control">
        <div class="flex justify-between">
          <label class="text-blue-900 font-medium" for="name">Name</label>
          <span
            v-if="errors.name"
            class="text-red-500 text-sm font-semibold"
          >
            {{ errors.name }}
          </span>
        </div>
        <q-input
          outlined
          placeholder="Name"
          v-model="form.name"
          :errorMessage="' '"
          noErrorIcon
          :rules="[val => !!val || (errors.name = 'Name is required')]"
        />
      </div>
      <div class="input-control">
        <div class="flex justify-between">
          <label class="text-blue-900 font-medium" for="name">Email</label>
          <span
            v-if="errors.email"
            class="text-red-500 text-sm font-semibold"
          >
            {{ errors.email }}
          </span>
        </div>
        <q-input
          outlined
          placeholder="Email"
          v-model="form.email"
          :errorMessage="' '"
          noErrorIcon
          :rules="[
            val => !!val || (errors.email = 'Email is required'),
            val => /.+@.+\..+/.test(val) || (errors.email = 'Invalid email')
          ]"
        />
      </div>
      <div class="input-control">
        <div class="flex justify-between">
          <label class="text-blue-900 font-medium" for="name">Phone</label>
          <span
            v-if="errors.phone"
            class="text-red-500 text-sm font-semibold"
          >
            {{ errors.phone }}
          </span>
        </div>
        <q-input
          outlined
          placeholder="Phone"
          v-model="form.phone"
          mask="(##) # ####-####"
          :errorMessage="' '"
          noErrorIcon
          :rules="[val => !!val || (errors.phone = 'Phone is required')]"
        />
      </div>
    </q-form>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { PropType } from 'vue'
import Title from '../Title.vue';

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

const errors = ref({
  name: '',
  email: '',
  phone: '',
})
</script>
