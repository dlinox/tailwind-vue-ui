<template>
  <div class="relative">
    <!-- Icono al principio -->
    <div class="flex items-center">
      <div
        v-if="$slots['icon-start']"
        class="absolute left-3 w-5 h-5 text-gray-600"
      >
        <slot name="icon-start" />
      </div>

      <select
        :value="inputValue"
        @change="updateValue"
        @blur="validateInput"
        class="border rounded-xl py-3 px-4 w-full appearance-none"
        :class="{
          'border-red-500': error,
          'pe-10': $slots['icon-end'],
          'ps-10': $slots['icon-start'],
        }"
      >
        <option
          v-for="option in options"
          :key="option.value"
          :value="option.value"
        >
          {{ option.label }}
        </option>
      </select>

      <!-- Icono al final -->
      <div
        v-if="$slots['icon-end']"
        class="absolute right-3 w-5 h-5 text-gray-600"
      >
        <slot name="icon-end" />
      </div>
    </div>

    <!-- Mensaje de error con transición -->
    <transition name="slide-fade">
      <div v-if="error" class="text-red-500 text-sm mt-1 origin-top">
        {{ error }}
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const props = defineProps({
  modelValue: [String, Number],
  required: Boolean,
  options: {
    type: Array,
    default: () => [],
  },
});

const emit = defineEmits(["update:modelValue"]);

const error = ref(null);

const inputValue = computed({
  get: () => props.modelValue,
  set: (value) => {
    emit("update:modelValue", value);
  },
});

const updateValue = (event) => {
  inputValue.value = event.target.value;
};

const validateInput = () => {
  validate(inputValue.value);
};

const validate = (value) => {
  error.value = null; // Resetear el mensaje de error

  // Verificar si es requerido
  if (props.required && !value) {
    error.value = "Debe seleccionar una opción.";
  }
};
</script>

<style scoped>
/* Estilos para la transición de deslizamiento y desvanecimiento */
.slide-fade-enter-from, .slide-fade-leave-to /* .slide-fade-leave-active in <2.1.8 */ {
  opacity: 0;
  transform: translateY(-1rem);
}
.slide-fade-enter-to,
.slide-fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

</style>
