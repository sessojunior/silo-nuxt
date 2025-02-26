<template>
  <div class="flex min-h-screen items-center justify-between">
    <div class="w-full md:w-1/2 md:max-w-[600px]">
      <div class="mx-auto w-full max-w-[330px] px-5">
        <slot />
      </div>
    </div>
    <div class="hidden min-h-screen flex-grow md:flex md:w-1/2 lg:w-1/2">
      <img src="/placeholder.svg" alt="Fundo" class="size-full h-screen object-cover" />
    </div>
    <div class="fixed bottom-5 right-5 z-20">
      <UiToggle
        aria-label="Trocar tema"
        @click="toggleColorMode"
        class="h-10 w-10 bg-background p-1 hover:text-black"
      >
        <Icon class="size-6" :name="colorMode.value === 'dark' ? 'ph:sun' : 'ph:moon'" />
      </UiToggle>
    </div>
  </div>
</template>

<script lang="ts" setup>
  const colorMode = useColorMode()
  const toggleColorMode = () => {
    colorMode.preference = colorMode.value === "dark" ? "light" : "dark"
  }
</script>
