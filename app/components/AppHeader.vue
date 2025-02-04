<script setup lang="ts">
const nuxtApp = useNuxtApp()
const { updateHeadings } = useScrollspy()

const links = computed(() => [
  {
    label: 'Услуги',
    to: '#services',
    active: false,
  },
  {
    label: 'Контакты',
    to: '#contacts',
    active: false,
  },
])

nuxtApp.hooks.hookOnce('page:finish', () => {
  updateHeadings([
    document.querySelector('#services'),
    document.querySelector('#contacts'),
  ])
})
</script>

<template>
  <UHeader :links="links">
    <template #logo>
      <!--      I.N. --><UBadge
        label="I.N."
        variant="subtle"
        class="mb-0.5"
      />
    </template>
    <template #right>
      <UColorModeButton size="sm" />
    </template>
  </UHeader>
</template>
