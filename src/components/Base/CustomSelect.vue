<template>
  <div class="relative">
    <div
      @click="open = !open"
      class="block w-full bg-white border rounded-xl p-3"
    >
      {{ selectedOption ? selectedOption.label : "Seleccione una opción" }}
    </div>
    <transition name="slide-fade">
      <div
        v-if="open"
        class="absolute w-full mt-2 bg-white border rounded shadow"
      >
        <div
          v-for="option in options"
          :key="option.value"
          @click="selectOption(option)"
          class="p-2 hover:bg-blue-50 cursor-pointer"
          :class="{ 'bg-blue-100 text-blue-800': option.value === modelValue }"
        >
          {{ option.label }}
        </div>
      </div>
    </transition>
  </div>
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
    const open = ref(false);
    const selectedOption = ref(
      props.options.find((o) => o.value === props.modelValue)
    );

    const selectOption = (option) => {
      selectedOption.value = option;
      emit("update:modelValue", option.value);
      open.value = false;
    };

    return {
      open,
      selectedOption,
      selectOption,
    };
  },
};
</script>

<style scoped>
/* Puedes agregar estilos adicionales si lo deseas */
</style>
