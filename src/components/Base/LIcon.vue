<template>
  <svg
    :class="`w-${size} h-${size}`"
    class="w-"
    xmlns="http://www.w3.org/2000/svg"
    fill="none"
    viewBox="0 0 24 24"
    stroke-width="1.5"
    stroke="currentColor"
    aria-hidden="true"
  >
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      :d="icons.filter((item) => item.name === icon)[0].icon"
    ></path>
  </svg>
</template>

<script setup>
import icons from "@/assets/icons.json";
const props = defineProps({
  icon: {
    type: String,
    required: true,
    validator: function (value) {
      // Define una lista de valores permitidos
      const allowedItems = icons.map((item) => item.name);

      // Comprueba si el valor del prop se encuentra en la lista permitida
      return allowedItems.includes(value);
    },
  },

  size: {
    type: [Number, String],
    default: 5,
  },
});
</script>
