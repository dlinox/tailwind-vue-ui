<template>
  <div v-for="option in options" :key="option.value" class="w-full">
    <input
      type="radio"
      :value="option.value"
      v-model="selectedValue"
      class="hidden"
      :id="`ra-${option.value}`"
    />
    <label
      :for="`ra-${option.value}`"
      class="flex items-center space-x-2 border-gray-300 border-2 p-2 mb-2 cursor-pointer ps-2 rounded-lg transition-all "
      :class="
        selectedValue === option.value
          ? ' border-blue-600 text-blue-600 '
          : 'bg-gray-50'
      "
    >
      <!-- Simular el aspecto del checkbox -->
      <span
        class="w-6 h-6 border  mr-2 flex items-center justify-center rounded-full"
      >
        <svg
          v-if="selectedValue === option.value"
          class="w-4 h-4 bg-blue-600  border-blue-600 border-2 rounded-full text-white"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M4.5 12.75l6 6 9-13.5"
          />
        </svg>
      </span>
      {{ option.label }}
    </label>
  </div>
</template>

<script>
import { computed } from "vue";
export default {
  props: {
    options: {
      type: Array,
      required: true,
    },
    modelValue: [String, Number, Object],
  },
  emits: ["update:modelValue"],
  setup(props, { emit }) {
    const selectedValue = computed({
      get: () => props.modelValue,
      set: (value) => {
        emit("update:modelValue", value);
      },
    });

    return {
      selectedValue,
    };
  },
};
</script>
  