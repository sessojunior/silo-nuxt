<template>
  <NuxtLayout name="login">
    <div class="flex min-h-screen items-center justify-between">
      <div class="w-full md:w-1/2">
        <div class="mx-auto w-full max-w-[330px] px-5">
          <h1 class="text-2xl font-bold tracking-tight lg:text-3xl">Entrar</h1>
          <p class="mt-1 text-muted-foreground">Digite seu e-mail e senha para entrar.</p>

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
              <UiDivider label="OU" />
              <UiButton variant="outline" type="button" @click="signInWithGoogle()">
                <Icon class="size-4" name="logos:google-icon" />
                <span>Continuar com Google</span>
              </UiButton>
            </fieldset>
          </form>
          <p class="mt-8 text-sm">
            <NuxtLink class="font-semibold text-primary underline-offset-2 hover:underline" to="#"
              >Esqueceu sua senha?</NuxtLink
            >
          </p>
          <p class="mt-4 text-sm text-muted-foreground">
            Não possui uma conta?
            <NuxtLink class="font-semibold text-primary underline-offset-2 hover:underline" to="#"
              >Crie uma agora</NuxtLink
            >
          </p>
        </div>
      </div>
      <div class="hidden min-h-screen md:block md:w-1/2 lg:w-1/2">
        <!-- eslint-disable-next-line vue/html-self-closing -->
        <img
          src="https://images.unsplash.com/photo-1512551980832-13df02babc9e?q=60&w=2864&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
          alt="Login form image"
          class="size-full min-h-screen object-cover"
        />
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
  </NuxtLayout>
</template>

<script lang="ts" setup>
  import { object, string } from "yup"
  import type { InferType } from "yup"

  useSeoMeta({
    title: "Log in",
    description: "Enter your email & password to log in.",
  })

  const colorMode = useColorMode()
  const toggleColorMode = () => {
    colorMode.preference = colorMode.value === "dark" ? "light" : "dark"
  }

  const isPasswordVisible = ref(false)
  const togglePasswordVisibility = () => (isPasswordVisible.value = !isPasswordVisible.value)

  const LoginSchema = object({
    email: string().email().required().label("Email"),
    password: string().required().label("Password").min(8),
  })

  const { handleSubmit, isSubmitting } = useForm<InferType<typeof LoginSchema>>({
    validationSchema: LoginSchema,
  })

  const submit = handleSubmit(async (_) => {
    useSonner("Logged in successfully!", {
      description: "You have successfully logged in.",
    })
  })

  const signInWithGoogle = () => {
    useSonner("Logged in successfully!", {
      description: "You have successfully logged in with Google.",
    })
  }
</script>
