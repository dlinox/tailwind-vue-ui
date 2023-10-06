<template>
  <div class="h-screen flex flex-col bg-gray-100 relative">
    <!-- Sidebar -->
    <aside
      :class="{
        'w-64 px-4': showSidebar,
        'w-0': !showSidebar,
      }"
      class="bg-white py-4 shadow-lg h-full transition-all duration-300 z-10 fixed overflow-x-hidden"
    >
      <h1 class="text-xl font-bold mb-4">Dashboard</h1>
      <ul>
        <li class="mb-2 hover:bg-gray-200 px-2 py-1 rounded">
          <a href="#">Inicio</a>
        </li>
        <li class="mb-2 hover:bg-gray-200 px-2 py-1 rounded">
          <a href="#">Reportes</a>
        </li>
        <li class="mb-2 hover:bg-gray-200 px-2 py-1 rounded">
          <a href="#">Configuración</a>
        </li>
      </ul>
    </aside>

    <div
      :class="{ ' block sm:hidden': showSidebar, hidden: !showSidebar }"
      class="fixed top-0 left-0 w-full h-full z-9 bg-slate-900 bg-opacity-20"
      @click="showSidebar = !showSidebar"
    ></div>

    <!-- Main content -->
    <div
      :class="{ 'ml-0 sm:ml-64': showSidebar, 'ml-0': !showSidebar }"
      class="flex-1 p-4 flex flex-col transition-all duration-300"
    >
      <main class="flex-1">
        <h2 class="text-2xl font-bold mb-4">Inicio</h2>
        <button
          @click="showSidebar = !showSidebar"
          class="bg-blue-500 p-2 text-white"
        >
          showSidebar
        </button>
        <h3 class="text-2xl uppercase my-4">component</h3>
        <div class="mb-5 px-5">
          <h5 class="text-xl uppercase my-3">#badges</h5>
          <div class="bg-white p-5 flex gap-2 items-end flex-wrap">
            <LBadges color="red" variant="outlined" density="sm" rounded="xl" />
            <LBadges color="blue" variant="tonal" density="sm" rounded="md" />
            <LBadges color="red" variant="tonal" density="md" rounded="sm" />
            <LBadges color="teal" variant="flat" density="md" rounded="md" />
            <LBadges color="blue" variant="text" density="md" rounded="sm" />
          </div>
        </div>

        <div class="mb-5 px-5">
          <h5 class="text-xl uppercase my-3">#buttons</h5>
          <div class="bg-white p-5 flex flex-wrap gap-2 items-end">
            <LButton
              @click="loadingBtn = !loadingBtn"
              :loading="loadingBtn"
              density="sm"
              color="blue"
              rounded="full"
              prepend-icon="M15.182 15.182a4.5 4.5 0 01-6.364 0M21 12a9 9 0 11-18 0 9 9 0 0118 0zM9.75 9.75c0 .414-.168.75-.375.75S9 10.164 9 9.75 9.168 9 9.375 9s.375.336.375.75zm-.375 0h.008v.015h-.008V9.75zm5.625 0c0 .414-.168.75-.375.75s-.375-.336-.375-.75.168-.75.375-.75.375.336.375.75zm-.375 0h.008v.015h-.008V9.75z"
              append-icon="M15.182 15.182a4.5 4.5 0 01-6.364 0M21 12a9 9 0 11-18 0 9 9 0 0118 0zM9.75 9.75c0 .414-.168.75-.375.75S9 10.164 9 9.75 9.168 9 9.375 9s.375.336.375.75zm-.375 0h.008v.015h-.008V9.75zm5.625 0c0 .414-.168.75-.375.75s-.375-.336-.375-.75.168-.75.375-.75.375.336.375.75zm-.375 0h.008v.015h-.008V9.75z"
            >
              asd
            </LButton>
            <LButton
              density="md"
              color="red"
              text="default"
              :loading="loadingBtn"
              @click="loadingBtn = !loadingBtn"
            />

            <LButton
              density="md"
              color="red"
              text="default"
              variant="outlined"
              @click="loadingBtn = !loadingBtn"
            />
            <LButton
              density="lg"
              color="blue"
              text="default"
              variant="outlined"
              :loading="loadingBtn"
              @click="loadingBtn = !loadingBtn"
            />

            <LButton
              disabled
              variant="variant"
              :loading="loadingBtn"
              @click="loadingBtn = !loadingBtn"
              density="block"
              color="blue"
              text="default"
              prepend-icon="M15.182 15.182a4.5 4.5 0 01-6.364 0M21 12a9 9 0 11-18 0 9 9 0 0118 0zM9.75 9.75c0 .414-.168.75-.375.75S9 10.164 9 9.75 9.168 9 9.375 9s.375.336.375.75zm-.375 0h.008v.015h-.008V9.75zm5.625 0c0 .414-.168.75-.375.75s-.375-.336-.375-.75.168-.75.375-.75.375.336.375.75zm-.375 0h.008v.015h-.008V9.75z"
            />
          </div>
        </div>

        <div class="mb-5 px-5">
          <h5 class="text-xl uppercase my-3">#CARD</h5>
          <div class="bg-gray-200 p-5 flex flex-wrap gap-2 items-end">
            <LCard title="title" sub-title="sub title">
              <template #card-body> sada </template>
              <template #card-footer>
                <div class="flex justify-between flex-wrap gap-3">
                  <LButton variant="tonal" color="red"> CANCELAR </LButton>
                  <LButton> ACEPTAR </LButton>
                </div>
              </template>
            </LCard>
          </div>
        </div>

        <div class="mb-5 px-5">
          <h5 class="text-xl uppercase my-3">#DIALOG</h5>
          <div class="bg-gray-200 p-5 flex flex-wrap gap-2 items-end">
            <LButton @click="showValue = !showValue"> Dialog</LButton>
            <LDialog v-model="showValue">
              <LCard title="modal" width="450px"> </LCard>
            </LDialog>
          </div>
        </div>

        <div class="mb-5 px-5">
          <h5 class="text-xl uppercase my-3">#EXPANTION PANEL</h5>
          <div class="bg-gray-200 p-5 flex flex-wrap gap-2 items-end">
            <LExpansionPanels
              v-model="panel1"
              title="panel"
              sub-title="sun titulo"
            />
            <LExpansionPanels
              v-model="panel2"
              title="panel"
              sub-title="sun titulo"
            />
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import LBadges from "./components/Base/LBadges.vue";
import LButton from "./components/Base/LButton.vue";
import LCard from "./components/Base/LCard.vue";
import LDialog from "./components/Base/LDialog.vue";
import LExpansionPanels from "./components/Base/LExpansionPanels.vue";

const showSidebar = ref(true);
const loadingBtn = ref(false);
const showValue = ref(false);

const panel1 = ref(false);
const panel2 = ref(false);
</script>
