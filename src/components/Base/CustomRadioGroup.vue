<template>

    <label
      v-for="option in options"
      :key="option.value"
      class="flex items-center space-x-2 border-gray-300 border-2 p-2 mb-2 cursor-pointer hover:border-blue-200 hover:bg-blue-100 hover:text-blue-800 ps-2 rounded-lg transition-all"
      :class="
        option.value === modelValue
          ? ' border-blue-200 text-blue-800 bg-blue-100'
          : 'bg-gray-50'
      "
      :for="`radio-${option.value}`"
    >
      <input
        :id="`radio-${option.value}`"
        type="radio"
        :value="option.value"
        v-model="selectedValue"
        @change="selectOption(option.value)"
        class="hidden"
      />
      <div :for="`radio-${option.value}`" class="flex items-center">
        <span
          class="w-6 h-6 border rounded-full mr-2 flex items-center justify-center"
          :class="option.value === modelValue ? '  bg-blue-600 text-white' : ''"
        >
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
              d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
            />
          </svg>
        </span>
        {{ option.label }}
      </div>
    </label>

</template>

<script>
import { ref } from "vue";
export default {
  props: {
    options: {
      type: Array,
      required: true,
    },
    modelValue: [String, Number],
  },
  emits: ["update:modelValue"],
  setup(props, { emit }) {
    const selectedValue = ref(props.modelValue);

    const selectOption = (value) => {
      emit("update:modelValue", value);
    };

    return {
      selectedValue,
      selectOption,
    };
  },
};
</script>
