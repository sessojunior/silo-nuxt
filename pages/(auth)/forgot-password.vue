<template>
  <NuxtLayout name="auth">
    <div
      class="mx-auto mb-6 flex size-14 items-center justify-center rounded-lg border bg-background"
    >
      <Icon class="size-6" name="lucide:key-round" />
    </div>
    <h1 class="text-center text-2xl font-bold tracking-tight lg:text-3xl">Esqueceu a senha</h1>
    <p class="mt-1 text-center text-muted-foreground">
      Não se preocupe, iremos te ajudar a recuperar sua senha.
    </p>
    <form class="mt-10" @submit="submit">
      <fieldset :disabled="isSubmitting" class="grid gap-5">
        <div>
          <UiVeeInput
            label="E-mail"
            type="email"
            name="email"
            placeholder="email@inpe.br"
            autocomplete="email"
          />
        </div>
        <div>
          <UiButton class="w-full" type="submit" text="Enviar instruções" />
        </div>
      </fieldset>
    </form>
    <p class="mt-8 text-center text-sm">
      <NuxtLink class="font-semibold text-primary underline-offset-2 hover:underline" to="/login"
        >Voltar e entrar</NuxtLink
      >
    </p>
  </NuxtLayout>
</template>

<script lang="ts" setup>
  import { object, string } from "yup"
  import type { InferType } from "yup"

  useSeoMeta({
    title: "Esqueceu a senha",
    description: "Digite seu e-mail para receber instruções de recuperação de senha.",
  })

  const LoginSchema = object({
    email: string()
      .email("E-mail inválido")
      .required("O e-mail é um campo obrigatório")
      .label("Email"),
  })

  const { handleSubmit, isSubmitting } = useForm<InferType<typeof LoginSchema>>({
    validationSchema: LoginSchema,
  })

  const submit = handleSubmit(async (values) => {
    console.log(values)
    useSonner("Confira seu e-mail", {
      description: "Enviamos um e-mail com instruções para redefinir sua senha.",
    })
  })
</script>
