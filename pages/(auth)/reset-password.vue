<template>
  <NuxtLayout name="auth">
    <div
      class="mx-auto mb-6 flex size-14 items-center justify-center rounded-lg border bg-background"
    >
      <Icon class="size-6" name="lucide:lock" />
    </div>
    <h1 class="text-center text-2xl font-bold tracking-tight lg:text-3xl">Nova senha</h1>
    <p class="mt-1 text-center text-muted-foreground">Digite sua nova senha abaixo.</p>
    <form class="mt-10" @submit="submit">
      <fieldset :disabled="isSubmitting" class="grid gap-5">
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
          <UiVeeInput
            label="Repita a senha"
            :type="isPasswordVisible ? 'text' : 'password'"
            name="confirmPassword"
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
  import { object, string, ref as yupRef } from "yup"
  import type { InferType } from "yup"

  useSeoMeta({
    title: "Nova senha",
    description: "Digite sua nova senha.",
  })

  const isPasswordVisible = ref(false)
  const togglePasswordVisibility = () => (isPasswordVisible.value = !isPasswordVisible.value)

  const LoginSchema = object({
    password: string()
      .required()
      .min(8, "A senha deve ter pelo menos 8 caracteres")
      .label("Senha")
      .test(
        "password",
        "A senha precisa ter pelo menos um número e um caractere especial",
        (value) => {
          return /^(?=.*[0-9])(?=.*[!@#$%^&*])[a-zA-Z0-9!@#$%^&*]{8,}$/.test(value)
        }
      ),
    confirmPassword: string()
      .required()
      .oneOf([yupRef("password")], "Senhas estão diferentes"),
  })

  const { handleSubmit, isSubmitting, meta } = useForm<InferType<typeof LoginSchema>>({
    validationSchema: LoginSchema,
  })

  const submit = handleSubmit(async (_) => {
    useSonner("Senha alterada", {
      description: "Sua senha foi alterada com sucesso.",
    })
  })
</script>
