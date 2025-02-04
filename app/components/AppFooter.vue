<script setup lang="ts">
</script>

<template>
  <UFooter>
    <template #left>
      <p class="text-gray-500 dark:text-gray-400 text-sm">
        Copyright © {{ new Date().getFullYear() }}. All rights reserved.
      </p>
    </template>

    <template #center>
      <ULink
        to="/terms"
        class="underline hover:text-blue-500 dark:hover:text-blue-400 transition-all duration-100 ease-in-out"
      >
        Terms of Service
      </ULink>
    </template>

    <template #right>
      <NuxtLink
        class="hover:text-primary underline underline-primary flex items-center justify-center"
        external
        target="_blank"
        to="https://https://t.me/irina_pro_wellness"
      >
        <UIcon name="i-logos:telegram" />
      </NuxtLink>
    </template>
  </UFooter>
</template>
