<template>
  <NuxtLayout name="admin">
    <div class="flex">
      <aside
        :class="`${openSidebar ? 'block max-w-60' : 'max-w-0'} ${openSidebarMobile ? '' : 'hidden'} h-screen border-r transition-all duration-300 sm:block`"
      >
        <div class="flex h-16 justify-between border-b">
          <div class="flex w-full items-center gap-2 px-4">
            <UiAvatar
              src="https://picsum.photos/200/400"
              alt="Company Logo"
              class="size-8 rounded object-contain"
            />
            <span class="text-xl font-bold">Silo</span>
          </div>
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
              <UiTooltipContent side="bottom" align="end">Ocultar menu lateral</UiTooltipContent>
            </UiTooltip>
          </div>
        </div>
        <UiScrollArea class="size-full h-[calc(100vh-128px)]">
          <div class="flex flex-col">
            <div class="my-6 px-4">
              <UiVeeInput v-model="search" placeholder="Procurar..." icon="lucide:search" />
            </div>
            <div class="flex h-full grow flex-col px-4">
              <div class="mb-8 flex flex-col">
                <div class="px-2 pb-2 text-xs font-medium uppercase text-muted-foreground">
                  Menu principal
                </div>
                <nav class="flex flex-col gap-1">
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
                <nav class="mt-auto flex flex-col gap-1">
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
              <div class="mb-4 mt-auto rounded-lg bg-muted/50 p-4 text-sm">
                <div class="flex items-center justify-between">
                  <p class="font-semibold">Used space</p>
                  <UiButton class="size-6" size="icon-sm" variant="ghost">
                    <Icon name="lucide:x" class="size-4 text-muted-foreground" />
                  </UiButton>
                </div>
                <p class="mt-3 text-muted-foreground">
                  Your team has used 80% of your available space. Need more?
                </p>
                <UiProgress class="my-4 h-2" :model-value="80" />
                <div class="flex items-center gap-1">
                  <UiButton class="px-2" variant="ghost" size="sm">Dismiss</UiButton>
                  <UiButton class="px-2 text-sky-500 hover:text-sky-600" variant="ghost" size="sm"
                    >Upgrade plan</UiButton
                  >
                </div>
              </div>
            </div>
          </div>
        </UiScrollArea>
        <div class="flex h-16 w-full items-center gap-2 border-t px-4">
          <div class="flex items-center gap-2">
            <UiAvatar :src="user.avatar" class="size-10" />
            <div>
              <p class="text-sm font-semibold leading-none" v-html="user.username" />
              <p class="text-xs text-muted-foreground" v-html="user.email" />
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
      </aside>
      <UiNavbar class="sticky top-0 z-20 h-16 w-full bg-background/90">
        <UiContainer class="flex h-full items-center justify-between">
          <div class="flex items-center">
            <div :class="`${openSidebar ? 'hidden' : 'flex'} items-center justify-center pr-2`">
              <UiTooltip>
                <UiTooltipTrigger as-child>
                  <UiButton
                    class="ml-auto shrink-0"
                    size="icon-sm"
                    variant="ghost"
                    @click="showSidebar"
                  >
                    <Icon name="lucide:panel-right-close" class="size-4 text-muted-foreground" />
                  </UiButton>
                </UiTooltipTrigger>
                <UiTooltipContent side="bottom" align="start">Exibir menu lateral</UiTooltipContent>
              </UiTooltip>
            </div>
            <div
              :class="`${openSidebarMobile ? 'hidden' : 'flex'} items-center justify-center pr-2 sm:hidden`"
            >
              <UiButton
                class="ml-auto shrink-0"
                size="icon-sm"
                variant="ghost"
                @click="showSidebarMobile"
              >
                <Icon name="lucide:panel-right-close" class="size-4 text-muted-foreground" />
              </UiButton>
            </div>
            <h2 class="font-semibold">Visão geral</h2>
          </div>
          <nav class="hidden items-center gap-5 sm:flex">
            <NuxtLink
              v-for="l in ['Home', 'About', 'Contact', 'Projects']"
              :key="l"
              class="text-sm text-muted-foreground transition-colors hover:text-foreground"
              to="/"
              >{{ l }}</NuxtLink
            >
          </nav>
        </UiContainer>
      </UiNavbar>
    </div>
  </NuxtLayout>
</template>

<script lang="ts" setup>
  const search = ref("")

  const openSidebar = ref(true)
  const openSidebarMobile = ref(false)
  const hideSidebar = () => (openSidebar.value = false)
  const showSidebar = () => (openSidebar.value = true)
  const showSidebarMobile = () => (openSidebarMobile.value = true)

  const user = {
    avatar: "https://randomuser.me/api/portraits/med/men/3.jpg",
    username: "Jane Doe",
    email: "muzcad@he.tg",
  }

  const topNav = [
    { title: "Home", icon: "lucide:home", link: "#" },
    {
      title: "Dashboard",
      icon: "lucide:bar-chart-3",
      items: [
        { title: "Overview", link: "#" },
        { title: "Notifications", link: "#" },
        { title: "Analytics", link: "#" },
        { title: "Reports", link: "#" },
      ],
    },
    { title: "Projects", icon: "lucide:folder-dot", link: "#" },
    { title: "Tasks", icon: "lucide:list-checks", link: "#" },
    { title: "Users", icon: "lucide:users", link: "#" },
  ]
  const bottomNav = [
    { title: "Support", icon: "lucide:life-buoy", link: "#" },
    {
      title: "Settings",
      icon: "lucide:settings-2",
      items: [
        { title: "Profile", link: "#" },
        { title: "Account", link: "#" },
        { title: "Security", link: "#" },
        { title: "Billing", link: "#" },
      ],
    },
  ]
</script>
