<template>
  <div class="relative">
    <div class="flex items-center">
      <!-- Icono al principio -->
      <div
        v-if="$slots['icon-start']"
        class="absolute left-3 w-5 h-5 text-gray-600"
      >
        <slot name="icon-start" />
      </div>

      <input
        v-model="inputValue"
        @blur="validateInput"
        class="border rounded-xl py-3 px-4 w-full"
        :class="{
          'border-red-500': error,
          'pe-10': $slots['icon-end'],
          'ps-10': $slots['icon-start'],
        }"
      />

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
      <div v-if="error" class="text-red-500 text-xs mt-1 px-3 origin-top">
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
  maxLength: Number,
  minLength: Number,
  exactLength: Number,
  type: {
    type: String,
    default: "integer",
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

const validateInput = () => {
  validate(props.modelValue);
};

const validate = (value) => {

  error.value = null; // Resetear el mensaje de error

  // 1. Verificar si es requerido
  if (props.required && !value) {
    error.value = "Este campo es requerido.";
    return;
  }

  // 2. Verificar longitud
  if (props.minLength && value.length < props.minLength) {
    error.value = `Debe tener al menos ${props.minLength} caracteres.`;
    return;
  }
  if (props.maxLength && value.length > props.maxLength) {
    error.value = `No debe exceder ${props.maxLength} caracteres.`;
    return;
  }
  if (props.exactLength && value.length !== props.exactLength) {
    error.value = `Debe tener exactamente ${props.exactLength} caracteres.`;
    return;
  }

  // 3. Verificar si es un número válido
  if (isNaN(value)) {
    error.value = "Debe ingresar un número válido.";
    return;
  }

  // 4. Verificar tipo de número
  if (props.type === "integer" && value.includes(".")) {
    error.value = "Solo se permiten números enteros.";
    return;
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
