<template>
  <NuxtLayout name="admin">
    <div class="flex w-full">
      <!-- Side left -->
      <div class="flex flex-grow flex-col">
        <!-- Graphs -->
        <div class="grid grid-cols-2 border-b border-b-[#F3F3F3]">
          <div class="flex flex-col border-r border-r-[#F3F3F3] px-8 py-6">
            <h3 class="pb-2 text-lg font-medium">Histórico de incidentes</h3>
            <div>Gráfico de coluna, com datas e porcentagens</div>
          </div>
          <div class="flex flex-col px-8 py-6">
            <h3 class="pb-2 text-lg font-medium">Causas de problemas</h3>
            <div>
              Gráfico radial, com os itens e a quantidade: Rede externa, Servidor indisponível,
              Falha humana, Rede interna, Erro no modelo, Outros problemas
            </div>
          </div>
        </div>

        <!-- Stats -->
        <div class="flex flex-col border-b border-b-[#F3F3F3] px-8 py-6">
          <h3 class="pb-2 text-lg font-medium">Status dos produtos</h3>
          <div class="flex flex-col">
            <div>Barra de progresso</div>
            <div>
              Legenda com os itens e quantidade: Em execução, Precisam de atenção, Com problemas
            </div>
          </div>
        </div>

        <!-- Products & tasks -->
        <div class="flex flex-col px-8 py-6">
          <h3 class="pb-2 text-lg font-medium">Produtos & tasks</h3>
          <div class="flex flex-col">
            <!-- Product item -->
            <div class="flex">
              <div class="flex">65%</div>
              <div class="flex">Produto 1</div>
              <div class="flex">Barra com status dos produtos</div>
              <div class="flex">Barra de progresso</div>
              <div class="flex">2h 43 min</div>
            </div>
            <!-- Product item -->
            <div class="flex">
              <div class="flex">84%</div>
              <div class="flex">Produto 2</div>
              <div class="flex">Barra com status dos produtos</div>
              <div class="flex">Barra de progresso</div>
              <div class="flex">38 min</div>
            </div>
            <!-- Product item -->
            <div class="flex">
              <div class="flex">21%</div>
              <div class="flex">Produto 3</div>
              <div class="flex">Barra com status dos produtos</div>
              <div class="flex">Barra de progresso</div>
              <div class="flex">30 min</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Side right -->
      <div
        class="hidden w-[420px] flex-shrink-0 flex-col border-l-2 border-l-[#F3F3F3] px-8 py-6 lg:flex"
      >
        <!-- Resume text -->
        <div class="flex flex-col border-b border-b-[#F3F3F3] pb-6">
          <h2 class="pb-4 text-xl font-medium">Resumo do dia</h2>
          <p class="text-sm">
            <span class="float-left mr-2">
              <span
                class="inline-flex h-8 w-8 items-center justify-center rounded-lg border border-yellow-200 bg-yellow-50"
                ><Icon class="size-4 text-yellow-500" name="lucide:lightbulb"
              /></span>
            </span>
            Hoje você tem <span class="rounded border px-1 py-0.5 font-medium">20%</span> mais
            problemas que o normal, você finalizou <strong>2 tasks</strong> em dois projetos, mas o
            foco está <span class="rounded border px-1 py-0.5 font-medium">12%</span> menor que
            ontem.
          </p>
        </div>

        <!-- Calendar activities -->
        <div class="flex flex-col border-b border-b-[#F3F3F3] py-6">
          <div>Calendário</div>
        </div>

        <!-- Activity resume -->
        <div class="grid grid-cols-2 border-b border-b-[#F3F3F3] py-6">
          <div>
            <h4 class="pb-2 text-sm font-light text-green-500">Processos rodando</h4>
            <div>
              <span class="text-xl font-medium">6h 18min</span>
            </div>
          </div>
          <div>
            <h4 class="pb-2 text-sm font-light text-red-500">Produtos parados</h4>
            <div>
              <span class="pr-2 text-xl font-medium">79%</span>
              <span class="text-sm">8h 9 min</span>
            </div>
          </div>
        </div>

        <!-- Radial Progress -->
        <div class="grid w-full grid-cols-4 border-b border-b-[#F3F3F3]">
          <div
            class="flex flex-col items-center justify-center border-r border-r-[#F3F3F3] px-2 py-6"
          >
            <div>62%</div>
            <div class="text-sm font-medium">Produtos</div>
          </div>
          <div
            class="flex flex-col items-center justify-center border-r border-r-[#F3F3F3] px-2 py-6"
          >
            <div>15%</div>
            <div class="text-sm font-medium">Processos</div>
          </div>
          <div
            class="flex flex-col items-center justify-center border-r border-r-[#F3F3F3] px-2 py-6"
          >
            <div>11%</div>
            <div class="text-sm font-medium">Projetos</div>
          </div>
          <div class="flex flex-col items-center justify-center px-2 py-6">
            <div>12%</div>
            <div class="text-sm font-medium">Outros</div>
          </div>
        </div>

        <!-- Ongoing projects -->
        <div class="flex flex-col py-6">
          <h3 class="pb-2 text-lg font-medium">Projetos em andamento</h3>
          <div class="flex flex-col">
            <!-- Project item -->
            <div class="flex flex-row">
              <div>58%</div>
              <div>Projeto 1</div>
              <div>Barra de progresso</div>
              <div>3h 43 min</div>
            </div>
            <!-- Project item -->
            <div class="flex flex-row">
              <div>32%</div>
              <div>Projeto 2</div>
              <div>Barra de progresso</div>
              <div>47 min</div>
            </div>
            <!-- Project item -->
            <div class="flex flex-row">
              <div>19%</div>
              <div>Projeto 3</div>
              <div>Barra de progresso</div>
              <div>31 min</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script setup lang="ts"></script>
