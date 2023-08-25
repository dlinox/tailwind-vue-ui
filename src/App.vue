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
        {{ showSidebar }}

        <button
          @click="showSidebar = !showSidebar"
          class="mb-4 bg-blue-500 text-white p-2 rounded"
        >
          {{ showSidebar ? "Ocultar" : "Mostrar" }} Sidebar
        </button>

        <LInputText
          v-model="textValue"
          :required="true"
          :minLength="5"
          :maxLength="10"
        >
          <template #icon-start>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
              />
            </svg>
          </template>
          <template #icon-end>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
              />
            </svg>
          </template>
        </LInputText>

        <LInputNumber
          v-model="inputN"
          :required="true"
          :minLength="5"
          :maxLength="10"
        >
        </LInputNumber>

        <LInputEmail
          v-model="inputE"
          :required="true"
          :minLength="5"
          :maxLength="10"
        >
          <template #icon-start>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                d="M16.5 12a4.5 4.5 0 11-9 0 4.5 4.5 0 019 0zm0 0c0 1.657 1.007 3 2.25 3S21 13.657 21 12a9 9 0 10-2.636 6.364M16.5 12V8.25"
              />
            </svg>
          </template>
        </LInputEmail>

        <LSelectInput
          v-model="inputS"
          :required="true"
          :options="[
            { label: 'Opción 1', value: '1' },
            { label: 'Opción 2', value: '2' },
            { label: 'Opción 3', value: '3' },
          ]"
        >
          <template #icon-start>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
              />
            </svg>
          </template>
          <template #icon-end>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </template>
        </LSelectInput>

        <CustomSelect
          :options="[
            { label: 'Opción 1', value: '1' },
            { label: 'Opción 2', value: '2' },
            { label: 'Opción 3', value: '3' },
          ]"
          v-model="selectedValue"
        />

        <CustomRadioGroup
          :options="[
            { label: 'Opción 1', value: '1' },
            { label: 'Opción 2', value: '2' },
            { label: 'Opción 3', value: '3' },
          ]"
          v-model="selectedRadioValue"
        />

        {{ selectedRadioValue }}

        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Pariatur
        necessitatibus obcaecati libero suscipit similique asperiores rerum
        culpa, explicabo, nam laudantium distinctio modi nesciunt quos aliquid
        voluptas quo non laborum sed?

        <Lcheckbox
          :options="[
            { label: 'Opción 1', value: '1' },
            { label: 'Opción 2', value: '2' },
            { label: 'Opción 3', value: '3' },
          ]"
          v-model="checkbox"

        />

        {{ checkbox }}

        <Lradiosss
          :options="[
            { label: 'Opción 1', value: '1' },
            { label: 'Opción 2', value: '2' },
            { label: 'Opción 3', value: '3' },
          ]"
          v-model="rass"

        />

        {{ rass }}
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import LInputNumber from "./components/Base/LInputNumber.vue";
import LInputText from "./components/Base/LInputText.vue";
import LInputEmail from "./components/Base/LInputEmail.vue";
import LSelectInput from "./components/Base/LSelectInput.vue";
import CustomSelect from "./components/Base/CustomSelect.vue";
import CustomRadioGroup from "./components/Base/CustomRadioGroup.vue";
import Lcheckbox from "./components/Base/checkbox.vue";
import Lradiosss from "./components/Base/radiosss.vue";

const textValue = ref("");
const inputN = ref(null);
const inputE = ref(null);
const inputS = ref(null);
const selectedValue = ref(null);
const selectedRadioValue = ref(null);
const showSidebar = ref(true);

const checkbox = ref([]);
const rass = ref(null);
</script>
