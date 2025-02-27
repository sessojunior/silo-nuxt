<template>
  <div class="relative flex">
    <!-- Column left -->
    <div
      :class="`${openSidebar ? 'left-0' : 'md:-left-60'} absolute -left-60 z-50 w-60 transition-all duration-300`"
    >
      <!-- Sidebar -->
      <aside class="h-screen w-full border-r bg-[#FEFEFE] sm:block">
        <!-- Sidebar Header -->
        <div class="flex h-16 justify-between border-b border-b-transparent bg-[#FEFEFE]">
          <div class="flex w-full items-center gap-2 px-4">
            <UiAvatar src="/logo.png" alt="Silo" class="size-8 rounded object-contain" />
            <span class="text-xl font-bold">Silo</span>
          </div>

          <!-- Button to hide sidebar -->
          <div class="flex items-center justify-center p-4">
            <UiTooltip>
              <UiTooltipTrigger as-child>
                <UiButton
                  class="ml-auto shrink-0"
                  size="icon-sm"
                  variant="ghost"
                  @click="hideSidebar"
                >
                  <Icon name="lucide:panel-right-open" class="size-4 text-muted-foreground" />
                </UiButton>
              </UiTooltipTrigger>
              <UiTooltipContent side="bottom" align="start">Ocultar menu lateral</UiTooltipContent>
            </UiTooltip>
          </div>
        </div>

        <!-- Sidebar Content -->
        <UiScrollArea class="size-full h-[calc(100vh-128px)]">
          <div class="flex flex-col">
            <!-- <div class="my-6 px-4">
                <UiVeeInput v-model="search" placeholder="Procurar..." icon="lucide:search" />
              </div> -->
            <div class="flex h-full grow flex-col px-4 pt-6">
              <div class="mb-8 flex flex-col">
                <div class="px-2 pb-2 text-xs font-medium uppercase text-muted-foreground">
                  Menu principal
                </div>
                <nav class="flex flex-col">
                  <template v-for="(n, i) in topNav" :key="i">
                    <UiButton
                      v-if="!n.items"
                      :to="n.link"
                      size="default"
                      variant="ghost"
                      class="justify-start gap-4 px-3"
                    >
                      <Icon v-if="n.icon" :name="n.icon" class="size-4 text-muted-foreground" />
                      <span>{{ n.title }}</span>
                    </UiButton>
                    <UiCollapsible v-if="n.items">
                      <UiCollapsibleTrigger as-child>
                        <UiButton
                          size="default"
                          variant="ghost"
                          class="group w-full justify-start gap-4 px-3"
                        >
                          <Icon v-if="n.icon" :name="n.icon" class="size-4 text-muted-foreground" />
                          <span>{{ n.title }}</span>
                          <Icon
                            name="lucide:chevron-down"
                            class="ml-auto size-4 text-muted-foreground transition group-data-[state=open]:rotate-180"
                          />
                        </UiButton>
                      </UiCollapsibleTrigger>
                      <UiCollapsibleContent class="flex flex-col pl-8 pr-2">
                        <template v-for="(item, index) in n.items" :key="index">
                          <UiButton
                            :to="item.link"
                            size="sm"
                            variant="ghost"
                            class="justify-start gap-4 px-3"
                          >
                            <span>{{ item.title }}</span>
                          </UiButton>
                        </template>
                      </UiCollapsibleContent>
                    </UiCollapsible>
                  </template>
                </nav>
              </div>
              <div class="mb-8 flex flex-col">
                <div class="px-2 pb-2 text-xs font-medium uppercase text-muted-foreground">
                  Outros
                </div>
                <nav class="mt-auto flex flex-col">
                  <template v-for="(n, i) in bottomNav" :key="i">
                    <UiButton
                      v-if="!n.items"
                      :to="n.link"
                      size="default"
                      variant="ghost"
                      class="justify-start gap-4 px-3"
                    >
                      <Icon v-if="n.icon" :name="n.icon" class="size-4 text-muted-foreground" />
                      <span>{{ n.title }}</span>
                    </UiButton>
                    <UiCollapsible v-if="n.items">
                      <UiCollapsibleTrigger as-child>
                        <UiButton
                          size="default"
                          variant="ghost"
                          class="group w-full justify-start gap-4 px-3"
                        >
                          <Icon v-if="n.icon" :name="n.icon" class="size-4 text-muted-foreground" />
                          <span>{{ n.title }}</span>
                          <Icon
                            name="lucide:chevron-down"
                            class="ml-auto size-4 text-muted-foreground transition group-data-[state=open]:rotate-180"
                          />
                        </UiButton>
                      </UiCollapsibleTrigger>
                      <UiCollapsibleContent class="flex flex-col pl-8 pr-2">
                        <template v-for="(item, index) in n.items" :key="index">
                          <UiButton
                            :to="item.link"
                            size="sm"
                            variant="ghost"
                            class="justify-start gap-4 px-3"
                          >
                            <span>{{ item.title }}</span>
                          </UiButton>
                        </template>
                      </UiCollapsibleContent>
                    </UiCollapsible>
                  </template>
                </nav>
              </div>
              <div class="mb-4 mt-auto rounded-lg bg-[#FAFAFA] p-4 text-sm">
                <div class="flex items-center justify-between">
                  <p class="font-semibold">O que há de novo?</p>
                  <UiButton class="size-6" size="icon-sm" variant="ghost">
                    <Icon name="lucide:x" class="size-4 text-muted-foreground" />
                  </UiButton>
                </div>
                <p class="text-medium mt-2 text-muted-foreground">
                  Confira as novidades dessa nova versão no dashboard.
                </p>
                <UiProgress class="mb-2 mt-4 h-2" :model-value="80" />
                <div class="flex items-center gap-1">
                  <UiButton class="px-2" variant="ghost" size="sm">Dispensar</UiButton>
                </div>
              </div>
            </div>
          </div>
        </UiScrollArea>

        <!-- Sidebar Footer -->
        <div class="flex h-16 justify-between border-t border-t-transparent">
          <div class="flex w-full items-center gap-2 px-4">
            <div class="flex items-center gap-2">
              <UiAvatar :src="user.avatar" class="size-10" />
              <div class="w-28">
                <p class="truncate text-sm font-medium leading-none" v-html="user.username" />
                <p class="truncate text-xs text-muted-foreground" v-html="user.team" />
              </div>
            </div>
            <UiTooltip>
              <UiTooltipTrigger as-child>
                <UiButton class="ml-auto shrink-0" size="icon-sm" variant="ghost">
                  <Icon name="lucide:log-out" class="size-4 text-muted-foreground" />
                </UiButton>
              </UiTooltipTrigger>
              <UiTooltipContent side="right" align="center">Deslogar</UiTooltipContent>
            </UiTooltip>
          </div>
        </div>
      </aside>
    </div>

    <!-- Column right -->
    <div
      :class="`${openSidebar ? 'md:left-60 md:w-[calc(100%-240px)]' : 'md:left-0 md:w-full'} absolute z-40 w-full transition-all duration-300`"
    >
      <!-- Topbar -->
      <div class="flex flex-col">
        <UiNavbar class="sticky top-0 h-16 w-full bg-muted/25">
          <div class="flex h-full items-center justify-between px-4">
            <div class="flex items-center">
              <!-- Button to show sidebar -->
              <div
                :class="`${openSidebar ? 'md:hidden' : 'md:flex'} hidden items-center justify-center pr-2`"
              >
                <UiTooltip>
                  <UiTooltipTrigger as-child>
                    <UiButton
                      class="ml-auto shrink-0"
                      size="icon-sm"
                      variant="ghost"
                      @click="showSidebar"
                    >
                      <Icon name="lucide:panel-right-open" class="size-4 text-muted-foreground" />
                    </UiButton>
                  </UiTooltipTrigger>
                  <UiTooltipContent side="bottom" align="start"
                    >Exibir menu lateral</UiTooltipContent
                  >
                </UiTooltip>
              </div>
              <!-- Button to show sidebar in mobile -->
              <div class="flex items-center justify-center pr-2 md:hidden">
                <UiTooltip>
                  <UiTooltipTrigger as-child>
                    <UiButton
                      class="ml-auto shrink-0"
                      size="icon-sm"
                      variant="ghost"
                      @click="showSidebar"
                    >
                      <Icon name="lucide:menu" class="size-5 text-muted-foreground" />
                    </UiButton>
                  </UiTooltipTrigger>
                  <UiTooltipContent side="bottom" align="start">Exibir menu</UiTooltipContent>
                </UiTooltip>
              </div>
              <h2 class="text-xl font-medium">Visão geral</h2>
            </div>
            <div class="flex items-center gap-4">
              <!-- Navigation Menu -->
              <div class="hidden items-center justify-center md:flex">
                <div class="flex gap-1">
                  <UiButton size="icon-sm" variant="ghost">
                    <Icon class="size-4" name="lucide:circle-help" />
                  </UiButton>
                  <UiButton size="icon-sm" variant="ghost">
                    <Icon class="size-4" name="lucide:activity" />
                  </UiButton>
                  <UiButton size="icon-sm" variant="ghost">
                    <Icon class="size-4" name="lucide:settings" />
                  </UiButton>
                </div>
                <UiDivider orientation="vertical" class="mx-2 h-6 w-2" />
                <UiChip color="bg-blue-500" size="md">
                  <UiButton size="icon-sm" variant="outline">
                    <Icon name="lucide:inbox" class="size-5" />
                  </UiButton>
                </UiChip>
                <UiDivider orientation="vertical" class="mx-2 h-6 w-2" />
                <div class="flex items-center gap-2">
                  <UiChip color="bg-teal-500" position="bottom-right">
                    <UiAvatar>
                      <UiAvatarImage :src="user.avatar" alt="Kelly King" />
                      <UiAvatarFallback>KK</UiAvatarFallback>
                    </UiAvatar>
                  </UiChip>
                  <div class="flex items-center">
                    <!-- <div class="w-28">
                      <p class="truncate text-sm font-medium leading-none" v-html="user.username" />
                      <p class="truncate text-xs text-muted-foreground" v-html="user.team" />
                    </div> -->

                    <!-- Dropdown Menu -->
                    <UiDropdownMenu>
                      <UiDropdownMenuTrigger as-child>
                        <UiButton class="ml-auto shrink-0" size="icon-xs" variant="ghost">
                          <Icon name="lucide:chevron-down" class="size-4 text-muted-foreground" />
                        </UiButton>
                      </UiDropdownMenuTrigger>
                      <UiDropdownMenuContent class="w-56" align="end">
                        <template v-for="(item, i) in dropdownMenuitems" :key="i">
                          <UiDropdownMenuLabel v-if="item.label" :label="item.label" class="py-2" />
                          <UiDropdownMenuSeparator v-else-if="item.divider" />
                          <UiDropdownMenuItem
                            v-else-if="item.title && !item.items"
                            :title="item.title"
                            :icon="item.icon"
                            :shortcut="item.shortcut"
                            :disabled="item.disabled"
                            class="cursor-pointer"
                          />
                          <UiDropdownMenuSub v-else-if="item.title && item.items">
                            <UiDropdownMenuSubTrigger
                              :title="item.title"
                              :icon="item.icon"
                              :text-value="item.title"
                              class="cursor-pointer"
                            />
                            <UiDropdownMenuSubContent>
                              <template v-for="(child, k) in item.items" :key="`child-${k}`">
                                <UiDropdownMenuSeparator v-if="child.divider" />
                                <UiDropdownMenuItem
                                  v-else
                                  :title="child.title"
                                  :icon="child.icon"
                                  :shortcut="child.shortcut"
                                  class="cursor-pointer"
                                />
                              </template>
                            </UiDropdownMenuSubContent>
                          </UiDropdownMenuSub>
                        </template>
                      </UiDropdownMenuContent>
                    </UiDropdownMenu>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </UiNavbar>
      </div>

      <!-- Content Main -->
      <div class="flex min-h-[calc(100vh-64px)] w-full">
        <slot />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
  const search = ref("")

  const openSidebar = ref(true)
  const showSidebar = () => {
    openSidebar.value = true
    console.log("openSidebar.value", openSidebar.value)
  }
  const hideSidebar = () => {
    openSidebar.value = false
    console.log("openSidebar.value", openSidebar.value)
  }

  onMounted(() => {
    console.log("openSidebar.value", openSidebar.value)
    console.log("window.innerWidth", window.innerWidth)
    if (window.innerWidth < 768) {
      openSidebar.value = false
    }
  })

  const user = {
    avatar: "https://randomuser.me/api/portraits/med/men/3.jpg",
    username: "Mario Junior",
    team: "Engenheiro de software",
  }

  const topNav = [
    { title: "Visão geral", icon: "lucide:home", link: "#" },
    {
      title: "Produtos & tasks",
      icon: "lucide:folder-check",
      items: [
        { title: "BAM", link: "#" },
        { title: "SMEC", link: "#" },
        { title: "BRAMS ams 15 km", link: "#" },
        { title: "WRF", link: "#" },
      ],
    },
    { title: "Projetos", icon: "lucide:folder-kanban", link: "#" },
    { title: "Grupos", icon: "lucide:users", link: "#" },
  ]

  const bottomNav = [
    { title: "Agenda", icon: "lucide:calendar-clock", link: "#" },
    { title: "Bate-papo", icon: "lucide:messages-square", link: "#" },
    {
      title: "Configurações",
      icon: "lucide:settings-2",
      items: [
        { title: "Alterar perfil", link: "#" },
        { title: "Preferências", link: "#" },
        { title: "Segurança", link: "#" },
      ],
    },
    { title: "Ajuda", icon: "lucide:life-buoy", link: "#" },
  ]

  const dropdownMenuitems = [
    { label: "Minha conta" },
    { divider: true },
    { title: "Profile", icon: "ph:user", shortcut: "⇧⌘P" },
    { title: "Billing", icon: "ph:credit-card", shortcut: "⌘B" },
    { title: "Settings", icon: "ph:gear", shortcut: "⌘S" },
    { title: "Keyboard shortcuts", icon: "ph:keyboard", shortcut: "⌘K" },
    { divider: true },
    { title: "Team", icon: "ph:users", shortcut: "⇧⌘T" },
    {
      title: "Invite Users",
      icon: "ph:user-plus",
      items: [
        { title: "Email", icon: "ph:envelope", shortcut: "⇧⌘E" },
        { title: "Facebook", icon: "logos:facebook", shortcut: "⇧⌘F" },
        { title: "Twitter", icon: "logos:twitter", shortcut: "⇧⌘T" },
        { divider: true },
        { title: "More", icon: "ph:plus-circle" },
      ],
    },
    { title: "Settings", icon: "ph:gear", shortcut: "⌘S" },
    { title: "Keyboard shortcuts", icon: "ph:keyboard", shortcut: "⌘K" },
    { divider: true },
    { title: "Github", icon: "ph:github-logo" },
    { title: "Support", icon: "ph:lifebuoy" },
    { title: "API", icon: "ph:cloud", disabled: true },
    { divider: true },
    { title: "Sign out", icon: "ph:sign-out" },
  ]
</script>
