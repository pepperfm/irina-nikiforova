<script setup lang="ts">
import type { InferType } from 'yup'
import { object, string } from 'yup'
import type { FormSubmitEvent } from '#ui/types'

const toast = useToast()
const services = [
  {
    title: 'Разбор анализов',
    icon: 'i-heroicons:magnifying-glass',
    class: 'col-span-4',
  },
  {
    title: 'Рекомендации по питанию и  нутрицевтической поддержке',
    icon: 'i-heroicons:book-open-20-solid',
    class: 'col-span-4',
  },
  {
    title: 'Разбор причин состояния',
    icon: 'i-heroicons:wrench-screwdriver-16-solid',
    class: 'col-span-4',
  },
]

const contact = ref({
  title: 'Связь со мной',
  description: 'Меня зовут Ирина, Я дипломированный превентивный нутрициолог☘️. Сделаю интерпретацию анализов, дам рекомендации по питанию, помогу найти причину причины проблем и справиться с ними. Бизнес-партнёр Siberian Wellness.❄️',
})
const { public: { baseApiUrl } } = useRuntimeConfig()
const carouselRef = ref()

onMounted(() => {
  setInterval(() => {
    if (!carouselRef.value)
      return

    if (carouselRef.value.page === carouselRef.value.pages) {
      return carouselRef.value.select(0)
    }

    carouselRef.value.next()
  }, 5000)
})

type Schema = InferType<typeof schema>
const loading = ref(false)
const RequiredText = 'Поле обязательно для заполнения'
const schema = object({
  email: string().email('Введите корректный адрес эл. почты'),
  text: string().required(RequiredText),
})
const state = reactive({
  email: undefined,
  text: undefined,
})
async function onSubmit(event: FormSubmitEvent<Schema>) {
  try {
    loading.value = true
    const { data, error } = await useFetch('/feedback', {
      baseURL: baseApiUrl,
      method: 'POST',
      body: event.data,
      watch: false,
    })
    const toastText: Partial<Notification> = {
      title: error.value ? 'Ошибка' : 'Фидбэк получили!',
      description: error?.value?.data?.message || data?.value?.message,
    }
    toast.add({
      ...toastText,
    })
    state.email = ''
    state.text = ''
  }
  catch (e) {
    console.error(e)
  }
  finally {
    loading.value = false
  }
}
</script>

<template>
  <div>
    <ULandingHero
      title="Ирина Никифорова"
      description="Нутрициолог | Бизнес-партнёр Siberian Wellness"
      class="bg-primary-50 dark:bg-primary-400 dark:bg-opacity-10"
    >
      <!-- ms:py-26 md:py-12 py-14 -->
      <NuxtImg
        format="webp"
        src="banner_omg.webp"
      />
    </ULandingHero>

    <ULandingSection id="services" title="Услуги">
      <ULandingGrid class="scroll-mt-[calc(var(--header-height)+140px+128px+96px)]">
        <ULandingCard
          v-for="(item, index) in services"
          :key="index"
          v-bind="item"
        />
      </ULandingGrid>
    </ULandingSection>

    <ULandingSection
      id="contacts"
      class="bg-primary-50 dark:bg-primary-400 dark:bg-opacity-10"
      :links="[
        {
          label: 'Связаться со мной',
          trailingIcon: 'i-logos:telegram',
          size: 'lg',
          external: true,
          to: 'https://t.me/Irinanutritionist',
          target: '_blank',
          variant: 'outline',
        },
      ]"
    >
      <ULandingCTA
        :title="contact.title"
        :description="contact.description"
        align="left"
        :card="false"
      >
        <div class="md:w-full">
          <UForm
            :schema="schema"
            :state="state"
            class="space-y-4 w-full"
            @submit="onSubmit"
          >
            <div class="flex flex-col md:flex-row gap-4">
              <UFormGroup
                class="w-full"
                required
                label="Email"
                name="email"
              >
                <UInput
                  v-model="state.email"
                  size="xl"
                  disabled
                />
              </UFormGroup>
            </div>
            <UFormGroup
              required
              label="Text"
              name="text"
            >
              <UTextarea
                v-model="state.text"
                size="xl"
                name="text"
                type="text"
                disabled
              />
            </UFormGroup>

            <UButton
              :loading="loading"
              label="Submit"
              type="submit"
              color="gray"
              variant="solid"
              disabled
            />
          </UForm>
        </div>
      </ULandingCTA>
    </ULandingSection>
  </div>
</template>
