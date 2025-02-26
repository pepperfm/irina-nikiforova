<script setup lang="ts">
</script>

<template>
  <UFooter>
    <template #left>
      <span>
        Created by PepperFM
      </span>
      <NuxtLink
        to="https://pepperfm.com"
        class="hover:text-primary transition ease-in-out delay-100 underline underline-primary flex items-center justify-center"
        external
        target="_blank"
        active-class="text-primary"
      >
        <UIcon name="simple-line-icons:globe" class="w-7 h-7" />
      </NuxtLink>
      <NuxtLink
        to="https://t.me/pepper_fm"
        class="hover:text-primary transition ease-in-out delay-100 underline underline-primary flex items-center justify-center"
        external
        target="_blank"
        active-class="text-primary"
      >
        <UIcon name="i-simple-icons:telegram" class="w-7 h-7" />
      </NuxtLink>
      <!--      <p class="text-gray-500 dark:text-gray-400 text-sm">
        Copyright © {{ new Date().getFullYear() }}. All rights reserved.
      </p> -->
    </template>

    <!--    <template #center>
      <ULink
        to="/terms"
        class="underline hover:text-blue-500 dark:hover:text-blue-400 transition-all duration-100 ease-in-out"
      >
        Terms of Service
      </ULink>
    </template> -->

    <template #right>
      <NuxtLink
        to="https://https://t.me/irina_pro_wellness"
        class="hover:text-primary underline underline-primary flex items-center justify-center"
        external
        target="_blank"
      >
        <UIcon name="i-simple-icons:telegram" class="w-7 h-7" />
      </NuxtLink>
    </template>
  </UFooter>
</template>
