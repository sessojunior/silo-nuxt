<template>
	<NuxtLayout name="auth">
		<div class="mx-auto mb-4 flex size-14 items-center justify-center rounded-lg border dark:border-neutral-700 dark:text-white">
			<Icon class="size-6" name="lucide:lock" />
		</div>
		<h1 class="text-3xl text-center font-bold tracking-tight dark:text-white">Nova senha</h1>
		<p class="mt-1 text-center text-sm dark:text-white">Digite sua nova senha abaixo.</p>
		<form class="mt-10">
			<fieldset class="grid gap-5">
				<!-- Strong Password -->
				<div>
					<label for="hs-strong-password-with-indicator-and-hint" class="block text-sm mb-2 dark:text-white">Nova senha</label>
					<div class="flex mb-2">
						<div class="flex-1">
							<div class="relative">
								<input type="password" placeholder="••••••••" autocomplete="current-password" required id="hs-strong-password-with-indicator-and-hint" class="hs-toggle-password py-3 px-4 block w-full border-gray-200 rounded-md text-sm focus:border-blue-500 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none dark:bg-neutral-900 dark:border-neutral-700 dark:text-neutral-400 dark:placeholder-neutral-500 dark:focus:ring-neutral-600" />
								<button
									type="button"
									data-hs-toggle-password='{
                "target": "#hs-strong-password-with-indicator-and-hint"
              }'
									class="absolute inset-y-0 end-0 flex items-center z-20 px-3 cursor-pointer text-gray-400 rounded-e-md focus:outline-none focus:text-blue-600 dark:text-neutral-600 dark:focus:text-blue-500"
								>
									<Icon name="lucide:eye" class="hidden hs-password-active:block size-4" />
									<Icon name="lucide:eye-off" class="hs-password-active:hidden size-4" />
								</button>
							</div>
							<div
								id="hs-strong-password"
								data-hs-strong-password='{
            "target": "#hs-strong-password-with-indicator-and-hint",
            "hints": "#hs-strong-password-hints",
            "stripClasses": "hs-strong-password:opacity-100 hs-strong-password-accepted:bg-teal-500 h-1 flex-auto rounded-full bg-blue-400 opacity-50 mx-1"
          }'
								class="flex mt-2 -mx-1"
							></div>
						</div>
					</div>
					<div id="hs-strong-password-hints" class="mb-2">
						<div class="mt-6 mb-2">
							<span class="text-sm font-semibold text-gray-800 dark:text-white">Força da senha: </span>
							<span data-hs-strong-password-hints-weakness-text='["Nenhuma", "Fraca", "Média", "Forte", "Muito forte", "Super forte"]' class="text-sm font-semibold text-gray-800 dark:text-neutral-200"></span>
						</div>
						<ul class="space-y-1 text-sm text-gray-500 dark:text-neutral-500">
							<li data-hs-strong-password-hints-rule-text="min-length" class="hs-strong-password-active:text-teal-500 flex items-center gap-x-2">
								<span class="hidden" data-check="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-check-big" class="size-4" />
									</span>
								</span>
								<span data-uncheck="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-x" class="size-4" />
									</span>
								</span>
								Precisa ter pelo menos 6 caracteres.
							</li>
							<li data-hs-strong-password-hints-rule-text="lowercase" class="hs-strong-password-active:text-teal-500 flex items-center gap-x-2">
								<span class="hidden" data-check="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-check-big" class="size-4" />
									</span>
								</span>
								<span data-uncheck="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-x" class="size-4" />
									</span>
								</span>
								Precisa ter letras minúsculas.
							</li>
							<li data-hs-strong-password-hints-rule-text="uppercase" class="hs-strong-password-active:text-teal-500 flex items-center gap-x-2">
								<span class="hidden" data-check="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-check-big" class="size-4" />
									</span>
								</span>
								<span data-uncheck="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-x" class="size-4" />
									</span>
								</span>
								Precisa ter letras maiúsculas.
							</li>
							<li data-hs-strong-password-hints-rule-text="numbers" class="hs-strong-password-active:text-teal-500 flex items-center gap-x-2">
								<span class="hidden" data-check="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-check-big" class="size-4" />
									</span>
								</span>
								<span data-uncheck="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-x" class="size-4" />
									</span>
								</span>
								Precisa coner números.
							</li>
							<li data-hs-strong-password-hints-rule-text="special-characters" class="hs-strong-password-active:text-teal-500 flex items-center gap-x-2">
								<span class="hidden" data-check="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-check-big" class="size-4" />
									</span>
								</span>
								<span data-uncheck="">
									<span class="flex justify-center items-center">
										<Icon name="lucide:circle-x" class="size-4" />
									</span>
								</span>
								Deve conter caracteres especiais.
							</li>
						</ul>
					</div>
				</div>

				<div>
					<button type="submit" class="w-full py-3 px-4 inline-flex justify-center items-center gap-x-2 text-sm font-medium rounded-lg border border-transparent bg-blue-600 text-white hover:bg-blue-700 focus:outline-none focus:bg-blue-700 disabled:opacity-50 disabled:pointer-events-none">Redefinir senha</button>
				</div>
			</fieldset>
		</form>
		<p class="mt-8 text-center text-sm">
			<NuxtLink class="font-semibold text-primary underline-offset-2 hover:underline dark:text-white" to="/login">Voltar e entrar</NuxtLink>
		</p>
	</NuxtLayout>
</template>

<script setup lang="ts"></script>
