<template>
  <div
    class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0"
  >
    <link
      href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css"
      rel="stylesheet"
    />
    <div class="max-w-4xl mx-auto sm:px-6 lg:px-8">
      <nuxt-link
        :to="localePath('/')"
        class="flex flex-row items-center justify-center"
      >
        <NuxtLogo />
        <div class="ml-2 text-2xl">Eonian Blog</div>
      </nuxt-link>
      <div class="mt-8 bg-white overflow-hidden shadow sm:rounded-lg p-6">
        <slot></slot>
      </div>
      <div class="flex justify-center pt-4 space-x-2">
        <GithubLink />
        <TwitterLink />
        <div class="flex">
          <nuxt-link
            v-for="locale in availableLocales"
            :key="locale"
            class="ml-2"
            :to="switchLocalePath(locale)"
            >{{ locale.toUpperCase() }}</nuxt-link
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'ThemeLayout',
  computed: {
    availableLocales() {
      return (this.$i18n.locales as string[]).filter(
        (i: string) => i !== this.$i18n.locale
      )
    },
  },
})
</script>
