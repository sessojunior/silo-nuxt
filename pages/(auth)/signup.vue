<template>
  <NuxtLayout name="auth">
    <UiAvatar src="/logo.png" alt="Silo" class="my-4 size-14 rounded object-contain" />
    <h1 class="text-2xl font-bold tracking-tight lg:text-3xl">Criar conta</h1>
    <p class="mt-1 text-muted-foreground">Crie uma conta e comece a usar.</p>
    <form class="mt-10" @submit="submit">
      <fieldset :disabled="isSubmitting" class="grid gap-5">
        <div>
          <UiVeeInput required label="Nome" name="name" placeholder="Fulano" />
        </div>
        <div>
          <UiVeeInput
            required
            label="E-mail"
            type="email"
            name="email"
            placeholder="email@inpe.br"
            autocomplete="email"
          />
        </div>
        <div>
          <UiVeeInput
            required
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
        <ul class="flex flex-col gap-3">
          <li class="flex items-center gap-2 text-sm text-muted-foreground">
            <Icon
              :class="[meta.valid ? 'text-green-500' : '']"
              class="size-5"
              name="lucide:check-circle-2"
            />
            <span>Deve ter pelo menos 8 caracteres</span>
          </li>
          <li class="flex items-center gap-2 text-sm text-muted-foreground">
            <Icon
              :class="[meta.valid ? 'text-green-500' : '']"
              class="size-5"
              name="lucide:check-circle-2"
            />
            <span>Deve ter número e caracter especial</span>
          </li>
        </ul>
        <div>
          <UiButton class="w-full" type="submit" text="Criar conta" />
        </div>
        <UiDivider label="ou" class="text-muted-foreground" />
        <div class="flex w-full flex-col items-center justify-center gap-3">
          <UiButton variant="outline" type="button" @click="signUpWithGoogle()" class="w-full">
            <Icon class="size-4" name="logos:google-icon" />
            <span>Criar com Google</span>
          </UiButton>
          <UiButton variant="outline" type="button" @click="signUpWithFacebook()" class="w-full">
            <Icon class="size-4" name="logos:facebook" />
            <span>Criar com Facebook</span>
          </UiButton>
        </div>
      </fieldset>
    </form>
    <p class="mt-8 text-center text-sm text-muted-foreground">
      Já possui uma conta?
      <NuxtLink class="font-semibold text-primary underline-offset-2 hover:underline" to="/login"
        >Entre agora</NuxtLink
      >
    </p>
  </NuxtLayout>
</template>

<script lang="ts" setup>
  import { object, string } from "yup"
  import type { InferType } from "yup"

  useSeoMeta({
    title: "Criar conta",
    description: "Crie uma conta e comece a usar.",
  })

  const isPasswordVisible = ref(false)
  const togglePasswordVisibility = () => (isPasswordVisible.value = !isPasswordVisible.value)

  const LoginSchema = object({
    name: string()
      .required("O nome é um campo obrigatório")
      .min(3, "O nome deve ter pelo menos 3 caracteres")
      .max(50, "O nome deve ter no máximo 50 caracteres")
      .label("Nome"),
    email: string()
      .email("E-mail inválido")
      .required("O e-mail é um campo obrigatório")
      .label("Email"),
    password: string()
      .required("A senha é um campo obrigatório")
      .label("Senha")
      .min(8, "A senha deve ter pelo menos 8 caracteres"),
  })

  const { handleSubmit, isSubmitting, meta } = useForm<InferType<typeof LoginSchema>>({
    validationSchema: LoginSchema,
  })

  const submit = handleSubmit(async (_) => {
    useSonner("Conta criada!", {
      description: "Você criou uma conta com sucesso.",
    })
  })

  const signUpWithGoogle = () => {
    useSonner("Vamos começar!", {
      description: "Você está sendo redirecionado ao Google...",
    })
  }

  const signUpWithFacebook = () => {
    useSonner("Vamos começar!", {
      description: "Você está sendo redirecionado ao Facebook...",
    })
  }
</script>
