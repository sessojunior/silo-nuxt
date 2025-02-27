<template>
  <NuxtLayout name="auth">
    <UiAvatar src="/logo.png" alt="Silo" class="my-4 size-14 rounded object-contain" />
    <h1 class="text-2xl font-bold tracking-tight lg:text-3xl">Entrar</h1>
    <p class="mt-1 text-muted-foreground">Digite seus dados para entrar.</p>
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
          <UiVeeInput
            label="Senha"
            :type="isPasswordVisible ? 'text' : 'password'"
            name="password"
            placeholder="••••••••"
            autocomplete="current-password"
          >
            <template #trailingIcon>
              <UiTooltip disable-closing-trigger>
                <UiTooltipTrigger as-child>
                  <button
                    type="button"
                    aria-label="Senha"
                    class="absolute inset-y-0 end-0 flex h-full w-9 items-center justify-center rounded-e-md border border-transparent text-muted-foreground/80 ring-offset-background transition-shadow hover:text-foreground focus-visible:border-ring focus-visible:text-foreground focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring/30 focus-visible:ring-offset-2 disabled:pointer-events-none disabled:cursor-not-allowed disabled:opacity-50"
                    @click="togglePasswordVisibility"
                  >
                    <Icon
                      :name="isPasswordVisible ? 'lucide:eye-off' : 'lucide:eye'"
                      class="size-4"
                    />
                  </button>
                </UiTooltipTrigger>
                <UiTooltipContent align="center">
                  {{ isPasswordVisible ? "Esconder" : "Mostrar" }} senha
                </UiTooltipContent>
              </UiTooltip>
            </template>
          </UiVeeInput>
        </div>
        <div>
          <UiButton class="w-full" type="submit" text="Entrar" />
        </div>
        <UiDivider label="ou" class="text-muted-foreground" />
        <div class="flex w-full flex-col items-center justify-center gap-3">
          <UiButton variant="outline" type="button" @click="signInWithGoogle()" class="w-full">
            <Icon class="size-4" name="logos:google-icon" />
            <span>Entrar com Google</span>
          </UiButton>
          <UiButton variant="outline" type="button" @click="signInWithFacebook()" class="w-full">
            <Icon class="size-4" name="logos:facebook" />
            <span>Entrar com Facebook</span>
          </UiButton>
        </div>
      </fieldset>
    </form>
    <p class="mt-8 text-sm">
      <NuxtLink
        class="font-semibold text-primary underline-offset-2 hover:underline"
        to="/forgot-password"
        >Esqueceu a senha?</NuxtLink
      >
    </p>
    <p class="mt-4 text-sm text-muted-foreground">
      Não possui uma conta?
      <NuxtLink class="font-semibold text-primary underline-offset-2 hover:underline" to="/signup"
        >Crie uma agora</NuxtLink
      >
    </p>
  </NuxtLayout>
</template>

<script lang="ts" setup>
  import { object, string } from "yup"
  import type { InferType } from "yup"

  useSeoMeta({
    title: "Entrar",
    description: "Digite seu e-mail e senha para entrar.",
  })

  const isPasswordVisible = ref(false)
  const togglePasswordVisibility = () => (isPasswordVisible.value = !isPasswordVisible.value)

  const LoginSchema = object({
    email: string()
      .email("E-mail inválido")
      .required("O e-mail é um campo obrigatório")
      .label("Email"),
    password: string()
      .required("A senha é um campo obrigatório")
      .label("Senha")
      .min(8, "A senha deve ter pelo menos 8 caracteres"),
  })

  const { handleSubmit, isSubmitting } = useForm<InferType<typeof LoginSchema>>({
    validationSchema: LoginSchema,
  })

  const submit = handleSubmit(async (_) => {
    useSonner("Emtrou com sucesso!", {
      description: "Você entrou no sistema com sucesso.",
    })
  })

  const signInWithGoogle = () => {
    useSonner("Emtrou com sucesso!", {
      description: "Você entrou no sistema com sucesso com o Google.",
    })
  }

  const signInWithFacebook = () => {
    useSonner("Emtrou com sucesso!", {
      description: "Você entrou no sistema com sucesso com o Facebook.",
    })
  }
</script>
