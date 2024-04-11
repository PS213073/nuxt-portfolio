
import { NuxtLink } from '#build/components';
<template>
  <div class="container mx-auto max-w-2xl">
    <header class="flex justify-between items-center mt-5">
      <div>
        <NuxtLink to="/" class="text-xl font-semibold p-2 hover:bg-gray-200"
          >Daniel Shahzada</NuxtLink
        >
      </div>
      <Menu />
    </header>
    <main class="p-2 mt-10">
      <slot />
    </main>
  </div>
</template>

<script setup>
const colorMode = useColorMode()
console.log(colorMode.preference)
colorMode.preference = 'light'
// colorMode.preference = 'dark'

useHead({
  titleTemplate: "%s - Daniel Shahzada",
  link: [
    {
      rel: "preconnect",
      href: "https://fonts.googleapis.com",
    },
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=Roboto&display=swap",
      crossorigin: "",
    },
  ],
});
</script>

<style>
body{
  /* font-family: Roboto; */
  @apply bg-white dark:bg-gray-900 text-gray-700 dark:text-gray-300
}
</style>