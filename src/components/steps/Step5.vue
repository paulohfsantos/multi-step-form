<template>
  <!-- div full height centered content -->
  <div class="flex flex-col items-center justify-center h-max">
    <div class="p-5 mt-24">
      <figure class="flex justify-center">
        <img :src="ThankYouImg" alt="celebration" />
      </figure>

      <div class="text-center">
        <h1 class="text-3xl font-bold text-blue-900 mt-8">Thank you!</h1>

        <p class="text-gray-400 mt-4">
          Thanks for confirming your subscription.
          We hope you have fun using our platform.
          If you ever need support, please feel free
          to email us at support@loremgaming.com
        </p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import ThankYouImg from '../../assets/images/icon-thank-you.svg'
</script>
