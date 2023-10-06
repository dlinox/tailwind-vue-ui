<template>
  <div class="bg-white w-full">
    <button
      v-if="$slots['card-header'] || title !== null || subTitle !== null"
      @click="emit('update:modelValue', !expandPanel)"
      class="relative text-start p-2 sm:px-3 sm:py-2 flex items-center flex-wrap w-full hover:bg-slate-50"
    >
      <div class="absolute right-2 bg-gray-50 p-1">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-5 h-5 transition-all duration-300"
          :class="expandPanel ? 'rotate-180' : ' '"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M19.5 8.25l-7.5 7.5-7.5-7.5"
          />
        </svg>
      </div>

      <h3 class="text-base font-semibold leading-7 text-gray-900 w-full">
        {{ title }}
      </h3>
      <p class="max-w-2xl text-sm leading-6 text-gray-500 w-full">
        {{ subTitle }}
      </p>
      <div class="w-full">
        <slot name="panel-header" />
      </div>
    </button>
    <div v-show="expandPanel" class="bg-gray-50 p-3 sm:p-4 overflow-hidden">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Officiis ratione
      doloremque temporibus molestias, provident sint tenetur sed! Doloremque
      eos consequuntur nihil voluptas, quia ea, voluptate, quo adipisci dolorem
      quibusdam delectus!
      <slot name="panel-body" />
    </div>

    <div v-if="$slots['card-footer']" class="bg-white p-2 sm:p-3">
      <slot name="panel-footer" />
    </div>
  </div>
</template>
<script setup>
import { computed } from "vue";

const props = defineProps({
  title: {
    type: String,
    default: null,
    required: true,
  },
  subTitle: {
    type: String,
    default: null,
  },
  modelValue: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["update:modelValue"]);

const expandPanel = computed({
  get: () => props.modelValue,
  set: (value) => {
    emit("update:modelValue", value);
  },
});
</script>
<style>
.df {
  transition: all;
}
</style>
