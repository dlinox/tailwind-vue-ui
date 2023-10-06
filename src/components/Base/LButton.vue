<template>
  <button
    :disabled="loading"
    :class="`${classDensity[density]}
      ${
        variant === 'flat'
          ? `bg-${color}-500 text-white`
          : variant === 'tonal'
          ? `bg-${color}-50 text-${color}-500`
          : variant === 'text'
          ? `text-${color}-500 `
          : variant === 'outlined'
          ? `border border-${color}-500 text-${color}-500 border-solid`
          : `bg-${color}-50 text-${color}-500`
      }
      rounded-${rounded}
      w-full xs:w-auto
      hover:bg-${color}-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-${color}-500
      `"
    class="relative disabled:text-gray-400 disabled:border-gray-100 disabled:cursor-not-allowed disabled"
  >
    <div class="flex gap-2.5 items-center justify-between">
      <div
        v-if="loading"
        class="absolute bg-slate-600/80 top-0 left-0 right-0 bottom-0 flex items-center justify-center"
        :class="`rounded-${rounded}`"
      >
        <div class="animate-spin">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-4 h-4"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0l3.181 3.183a8.25 8.25 0 0013.803-3.7M4.031 9.865a8.25 8.25 0 0113.803-3.7l3.181 3.182m0-4.991v4.99"
            />
          </svg>
        </div>
      </div>
      <div>
        <LIcon
          v-if="prependIcon"
          :class="`${classDensityIcon[density]}`"
          :path="prependIcon"
        />
      </div>

      <div class="">
        <slot />
        {{ text }}
      </div>
      <div>
        <LIcon
          v-if="appendIcon"
          :class="`${classDensityIcon[density]}`"
          path="M15.182 15.182a4.5 4.5 0 01-6.364 0M21 12a9 9 0 11-18 0 9 9 0 0118 0zM9.75 9.75c0 .414-.168.75-.375.75S9 10.164 9 9.75 9.168 9 9.375 9s.375.336.375.75zm-.375 0h.008v.015h-.008V9.75zm5.625 0c0 .414-.168.75-.375.75s-.375-.336-.375-.75.168-.75.375-.75.375.336.375.75zm-.375 0h.008v.015h-.008V9.75z"
        />
      </div>
    </div>
  </button>
</template>
<script setup>
import { ref } from "vue";
import LIcon from "./LIcon.vue";

const props = defineProps({
  density: {
    type: String,
    default: "md",
  },
  color: {
    type: String,
    default: "blue",
  },
  rounded: {
    type: String,
    default: "md",
  },
  variant: {
    type: String,
    default: "flat",
  },
  text: {
    type: String,
  },

  loading: {
    type: true,
    default: false,
  },

  prependIcon: {
    type: String,
  },

  appendIcon: {
    type: String,
  },
});

const classDensity = ref({
  sm: "px-2.5 py-1.5 text-sm",
  md: "px-3 py-1.5 text-md",
  lg: "px-3.5 py-2 text-lg",
  xl: "px-4 py-2.5 text-xl",
  block: "w-full px-4 py-2.5 text-xl",
});

const classDensityIcon = ref({
  sm: "h-4 w-4",
  md: "h-5 w-5",
  lg: "h-6 w-6",
  xl: "h-7 w-7",
});
</script>
