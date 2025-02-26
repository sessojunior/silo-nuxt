<template>
  <NuxtLayout name="auth">
    <div
      class="mx-auto mb-6 flex size-14 items-center justify-center rounded-lg border bg-background"
    >
      <Icon class="size-6" name="lucide:mail" />
    </div>
    <h1 class="text-center text-2xl font-bold tracking-tight lg:text-3xl">Confira seu e-mail</h1>
    <p class="mt-1 text-center text-muted-foreground">
      Enviamos um e-mail com instruções para redefinir sua senha.
    </p>
    <div class="mt-10">
      <UiButton to="/forgot-password" class="w-full" type="submit">
        <Icon class="size-5" name="lucide:arrow-left" />
        <span>Reenviar instruções</span>
      </UiButton>
    </div>
    <p class="mt-8 text-center text-sm">
      <NuxtLink class="font-semibold text-primary underline-offset-2 hover:underline" to="/login"
        >Voltar e entrar</NuxtLink
      >
    </p>
  </NuxtLayout>
</template>

<script lang="ts" setup>
  useSeoMeta({
    title: "Confira seu e-mail",
    description: "Enviamos um e-mail com instruções para redefinir sua senha.",
  })
</script>
