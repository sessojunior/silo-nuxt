<template>
  <NuxtLayout name="auth">
    <div
      class="mx-auto mb-6 flex size-14 items-center justify-center rounded-lg border bg-background"
    >
      <Icon class="size-6" name="lucide:square-asterisk" />
    </div>
    <h1 class="text-center text-2xl font-bold tracking-tight lg:text-3xl">Verificar conta</h1>
    <p class="mt-1 text-center text-muted-foreground">
      Insira abaixo o código de verificação enviado para seu e-mail.
    </p>
    <form class="mt-10" @submit="submit">
      <fieldset :disabled="isSubmitting" class="grid gap-5">
        <div>
          <UiLabel class="flex flex-col items-start">
            <p class="mb-3 text-sm font-medium">Código de verificação</p>
            <UiPinInput name="code" placeholder="" :input-count="5" />
          </UiLabel>
        </div>
        <div>
          <UiButton class="w-full" type="submit" text="Verificar conta" />
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
    title: "Verificar conta",
    description: "Digite o código enviado para seu e-mail.",
  })

  const LoginSchema = object({
    code: string()
      .email("Código de verificação inválido")
      .required("O código de verificação é um campo obrigatório")
      .label("Código de verificação"),
  })

  const { handleSubmit, isSubmitting } = useForm<InferType<typeof LoginSchema>>({
    validationSchema: LoginSchema,
  })

  const submit = handleSubmit(async (values) => {
    console.log(values)
    useSonner("Verificação completa", {
      description: "Sua conta foi verificada com sucesso.",
    })
  })
</script>
